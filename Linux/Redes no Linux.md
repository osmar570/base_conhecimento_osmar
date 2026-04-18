# Redes no Linux (Networking Profundo)

O Linux é o "rei da rede". Seu stack TCP/IP é extremamente eficiente e configurável. Entender como manipular interfaces, tabelas de roteamento e firewalls é essencial para gerenciar servidores e clusters de containers.

---

## 1. Comandos de Inspeção e Diagnóstico

Esqueça o antigo `ifconfig` (depreciado). Use a moderna suíte `iproute2`.

### Gerenciamento de Interfaces e IPs
*   **`ip addr`**: Lista todas as interfaces de rede e seus endereços IP.
*   **`ip link set eth0 up/down`**: Ativa ou desativa uma interface de rede.
*   **`ip route show`**: Exibe a tabela de roteamento (por onde os pacotes saem).

### Verificação de Portas e Conexões
*   **`ss -tulpn`**: O sucessor do `netstat`. Mostra quais portas estão abertas e qual processo (PID) as está usando.
    *   `-t`: TCP / `-u`: UDP / `-l`: Listening / `-p`: Process / `-n`: Numérico (não resolve nomes).
*   **`lsof -i :80`**: Mostra exatamente quem está usando a porta 80.

### Testes de Conectividade
*   **`ping -c 4 google.com`**: Testa latência básica.
*   **`traceroute google.com`**: Mostra o caminho (saltos) que o pacote faz até o destino.
*   **`dig google.com`**: Ferramenta definitiva para depurar DNS.
*   **`curl -Iv https://google.com`**: Verifica cabeçalhos HTTP e certificados SSL.

---

## 2. Gerenciamento de Portas e Firewall

No Linux moderno (Ubuntu/Debian), o firewall padrão é o **UFW** (Uncomplicated Firewall), que simplifica as regras complexas do `iptables` ou `nftables`.

### Com o UFW (Recomendado para iniciantes/médios)
*   **Status:** `sudo ufw status`
*   **Abrir Porta:** `sudo ufw allow 80/tcp`
*   **Fechar Porta:** `sudo ufw deny 80/tcp`
*   **Permitir SSH:** `sudo ufw allow ssh` (Porta 22)
*   **Ativar Firewall:** `sudo ufw enable`

### Com IPTables (Nível Especialista)
O `iptables` manipula as tabelas do kernel diretamente.
*   **Bloquear um IP específico:**
    `sudo iptables -A INPUT -s 1.2.3.4 -j DROP`
*   **Redirecionar porta 80 para 8080 (Port Forwarding):**
    `sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080`

---

## 3. Arquivos de Configuração Críticos

*   **`/etc/hosts`**: Mapeamento local de nomes para IPs (seu DNS privado).
*   **`/etc/resolv.conf`**: Configuração dos servidores DNS que o sistema usa (ex: 8.8.8.8).
*   **`/etc/ssh/sshd_config`**: Onde você muda a porta do SSH ou desativa o login de root para segurança.

---

## 4. Plugins e Ferramentas Poderosas

Para um monitoramento de rede avançado, instale estas ferramentas:

1.  **`nmap`**: O "canivete suíço" da rede. Escaneia portas abertas em outros servidores.
    *   `nmap -sV 192.168.1.1` (Descobre serviços rodando no IP).
2.  **`tcpdump`**: Analisador de pacotes via linha de comando. Permite ver o tráfego bruto passando pela placa de rede.
    *   `sudo tcpdump -i eth0 port 80`
3.  **`iftop`**: Mostra o consumo de banda por conexão em tempo real (como um `top` para rede).
4.  **`nload`**: Gráfico visual do tráfego de entrada e saída.
5.  **`mtr`**: Combina `ping` e `traceroute` em uma ferramenta de diagnóstico contínuo.

---

## 💡 Cenário Prático (DevOps)
**Problema:** Seu container Docker está rodando na porta 3000, mas você não consegue acessar de fora.
1.  Verifique se o processo está ouvindo: `ss -tulpn | grep 3000`.
2.  Verifique se o firewall está bloqueando: `sudo ufw status`.
3.  Teste a conectividade local: `curl localhost:3000`.
4.  Verifique se o redirecionamento de portas do Docker está ativo no `iptables`: `sudo iptables -L -n -t nat`.

---
**Links Relacionados:**
- [[Linux]]
- [[Redes no Docker]] (O Docker cria pontes virtuais sobre a rede do Linux)
- [[Kubernetes]] (Usa CNI - Container Network Interface)
