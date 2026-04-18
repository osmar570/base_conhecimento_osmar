# SSH e Acesso Remoto Seguro

O **SSH (Secure Shell)** é o protocolo padrão para acessar e gerenciar servidores Linux de forma criptografada. Dominar o SSH é a habilidade número 1 de qualquer profissional de infraestrutura.

---

## 1. Gerenciamento de Chaves (A forma segura)

Usar senhas para acessar servidores é inseguro e ineficiente. O padrão ouro é o uso de **Chaves Assimétricas** (Pública e Privada).

### Gerando suas chaves
No seu computador local:
```bash
ssh-keygen -t ed25519 -C "seu_email@exemplo.com"
```
*Isso criará dois arquivos em `~/.ssh/`: `id_ed25519` (Sua chave PRIVADA - nunca compartilhe) e `id_ed25519.pub` (Sua chave PÚBLICA).*

### Enviando a chave para o servidor
```bash
ssh-copy-id usuario@ip-do-servidor
```
*A partir de agora, você entrará no servidor sem precisar digitar senha.*

---

## 2. O arquivo de configuração (`~/.ssh/config`)

Se você gerencia muitos servidores, decorar IPs é impossível. O Linux permite criar "apelidos" no arquivo local `~/.ssh/config`.

**Exemplo de configuração:**
```text
Host producao
    HostName 104.24.1.50
    User osmar
    Port 2222
    IdentityFile ~/.ssh/id_ed25519

Host banco-dados
    HostName db.minhaempresa.com
    User admin
```

**Como usar:** Basta digitar `ssh producao` e o sistema aplicará todas as configurações automaticamente.

---

## 3. Segurança Bruta (Hardening)

Para proteger seu servidor de ataques de força bruta, edite o arquivo `/etc/ssh/sshd_config` no servidor:

1.  **Desativar login de Root:** `PermitRootLogin no`
2.  **Desativar login por senha:** `PasswordAuthentication no` (Só entra quem tem chave cadastrada).
3.  **Mudar a porta padrão (22):** `Port 2222` (Opcional, mas ajuda a reduzir logs de robôs).

*Após mudar, reinicie o serviço: `sudo systemctl restart ssh`.*

---

## 4. Ferramentas para Gerenciar Múltiplos Servidores

### A. Para uso Manual (GUI/Terminal)
*   **Termius (Recomendado):** Uma ferramenta moderna (desktop e mobile) que organiza seus servidores em grupos, sincroniza suas chaves na nuvem de forma segura e permite rodar comandos em vários servidores ao mesmo tempo.
*   **MobaXterm (Windows):** Um "canivete suíço" com terminal, SFTP visual e suporte a X11 embutido.
*   **Tmux + ClusterSSH:** Ferramentas de terminal puro que permitem abrir 10 janelas de servidores diferentes e digitar o mesmo comando em todos simultaneamente.

### B. Para Automação (Infraestrutura como Código)
*   **Ansible:** Se você tem 50 servidores, você não entra neles um por um. Você escreve um "Playbook" e o Ansible usa o SSH para entrar em todos e executar as tarefas (instalar pacotes, configurar usuários, etc.) automaticamente.

---

## 5. Transferência de Arquivos via SSH

*   **SCP:** `scp arquivo.txt usuario@ip:/home/usuario/` (Copia um arquivo rápido).
*   **RSYNC (Melhor):** `rsync -avz pasta/ usuario@ip:/home/usuario/` (Copia apenas o que mudou, economizando banda e tempo).

---
**Links Relacionados:**
- [[Linux]] (Início)
- [[Redes no Linux]] (Portas e Firewall)
- [[Terraform]] (Onde você geralmente injeta sua chave pública na criação do servidor)
