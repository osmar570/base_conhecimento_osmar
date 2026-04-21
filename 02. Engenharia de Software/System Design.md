# System Design (Design de Sistemas)

System Design é o processo de definir a arquitetura macro de um sistema para suportar requisitos extremos de carga, garantindo resiliência e baixa latência através de trade-offs conscientes.

---

## 🏗️ 1. Escalabilidade: Horizontal vs Vertical

- **Vertical (Scale-Up):** Aumentar recursos (CPU, RAM) de um único servidor.
    - *Limite:* Há um teto físico e financeiro, além de ser um ponto único de falha.
- **Horizontal (Scale-Out):** Adicionar mais máquinas ao pool.
    - *Desafio:* Exige que a aplicação seja **Stateless** (o estado deve estar em um cache externo ou banco, não na memória da instância).

---

## ⚖️ 2. Load Balancing (Balanceamento de Carga)

Distribui requisições para evitar gargalos em instâncias específicas.

### Camadas de Atuação:
- **Layer 4 (Transport):** Baseado em IP e Porta TCP/UDP. É extremamente rápido pois não abre o pacote de dados.
- **Layer 7 (Application):** Baseado em URLs, Cookies e Headers. Permite roteamento inteligente (ex: `/api/v1` vai para o Cluster A, `/api/v2` vai para o B).

### Algoritmos Comuns:
- **Round Robin:** Distribuição sequencial simples.
- **Least Connections:** Envia para quem está menos ocupado.
- **IP Hash:** Mapeia o IP do cliente para o mesmo servidor (útil para sessões persistentes/sticky sessions).

---

## ⚡ 3. Caching em Profundidade

O cache deve ser aplicado em múltiplas camadas para reduzir o IOPS do banco de dados.

### Estratégias de Escrita:
1.  **Cache Aside (Lazy Loading):** A aplicação busca no cache; se não achar (cache miss), busca no banco e atualiza o cache.
2.  **Write-Through:** Os dados são escritos no cache e no banco simultaneamente. Garante consistência, mas aumenta a latência de escrita.
3.  **Write-Behind (Write-Back):** Escreve no cache e o cache sincroniza com o banco de forma assíncrona. Altíssima performance, mas risco de perda de dados se o cache cair.

### Políticas de Evicção (Quando o cache enche):
- **LRU (Least Recently Used):** Remove o que não é usado há mais tempo.
- **LFU (Least Frequently Used):** Remove o que é menos acessado em volume.
- **FIFO (First In, First Out):** Fila simples.

---

## 🗄️ 4. Persistência e Replicação de Dados

Em escala, um único banco de dados se torna o maior gargalo do sistema.

### Replicação:
- **Master-Slave (Read Replicas):** Escritas vão para o Master, Leituras para os Slaves. Aumenta performance de leitura.
- **Master-Master:** Múltiplos nós aceitam escrita. Extremamente complexo para resolver conflitos de ID e consistência.

### Particionamento (Sharding):
- **Range Based:** Particiona por intervalos (ex: Usuários de A-M no DB1, N-Z no DB2).
- **Hash Based:** Aplica uma função hash no ID do usuário para decidir em qual banco ele vive (distribuição mais uniforme).

---

## 🛰️ 5. Proxies: Forward vs Reverse

- **Forward Proxy:** Fica "na frente" dos clientes. Usado para anonimato, filtros de conteúdo e controle de saída de rede.
- **Reverse Proxy (Nginx, Envoy):** Fica "na frente" dos servidores. Usado para terminação SSL, compressão gzip e segurança (esconde a topologia interna da rede).

---

## 📉 6. Disponibilidade e Redundância

- **SLA (Service Level Agreement):**
    - **99.9% (3 noves):** ~9 horas de downtime/ano.
    - **99.999% (5 noves):** ~5 minutos de downtime/ano (padrão ouro).
- **Failover:**
    - **Active-Passive:** O servidor reserva assume apenas se o principal cair.
    - **Active-Active:** Todos os servidores processam carga simultaneamente.

---
**Links Relacionados:**
- [[02. Engenharia de Software/Bancos de Dados|Bancos de Dados e CAP]]
- [[02. Engenharia de Software/Mensageria e Eventos|Mensageria e Desacoplamento]]
- [[03. Plataforma e Cloud-Native/Kubernetes/Autoscaling no Kubernetes|Escalabilidade Automática]]
