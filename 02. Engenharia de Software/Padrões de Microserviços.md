# Padrões de Microserviços

A adoção de microserviços traz agilidade, mas aumenta a complexidade. O uso de padrões arquiteturais é essencial para gerenciar a consistência de dados e a comunicação entre componentes.

---

## 🏛️ Padrões de Gerenciamento de Dados

### 1. CQRS (Command Query Responsibility Segregation)
Separação da responsabilidade de escrita (Comandos) da responsabilidade de leitura (Consultas).
- **Comandos:** Focam na lógica de negócio e validação.
- **Consultas:** Focam na performance e projeção de dados (muitas vezes usando bancos diferentes, ex: Escrita em SQL e Leitura em NoSQL/Elasticsearch).
- **Benefício:** Permite escalar leitura e escrita independentemente.

### 2. Event Sourcing
Em vez de armazenar o estado atual do objeto, armazenamos a **sequência de eventos** que levou a esse estado.
- O estado atual é reconstruído "reproduzindo" os eventos.
- **Benefício:** Auditoria perfeita e capacidade de reconstruir o estado em qualquer ponto do tempo.

---

## 🛰️ Padrões de Exposição e Consumo

### 1. API Gateway
Um ponto de entrada único para todas as requisições dos clientes.
- **Responsabilidades:** Autenticação, Rate Limiting, Roteamento, Logging e Caching.
- **Benefício:** Esconde a complexidade interna do cluster (K8s) para o cliente externo.

### 2. BFF (Backend for Frontend)
Uma variação do API Gateway onde criamos um backend específico para cada tipo de cliente (ex: um para Mobile, outro para Web).
- **Benefício:** Otimiza o payload para as necessidades específicas de cada tela, evitando over-fetching.

---

## 🔄 Resiliência e Consistência

- **Saga Pattern:** Gerencia transações distribuídas entre microserviços. Se um passo falhar, a Saga executa ações de compensação para manter a consistência.
- **Circuit Breaker:** Impede que uma falha em um serviço em cascata derrube todo o sistema, interrompendo chamadas para serviços que estão comprovadamente lentos ou fora do ar.

---
**Links Relacionados:**
- [[02. Engenharia de Software/Mensageria e Eventos|Mensageria e Eventos]] (O transporte para CQRS e Sagas)
- [[02. Engenharia de Software/Clean Architecture/Clean Architecture|Clean Architecture]] (Organização interna de cada microserviço)
- [[05. Trilhas de Estudos/Arquiteto de Software|Trilha de Arquiteto]] (Decisões de macro-arquitetura)
