# Comandos Essenciais de Terminal

O terminal (ou shell) é onde a mágica do Linux acontece. Dominar estes comandos é fundamental para qualquer desenvolvedor ou administrador de sistemas.

---

## 1. Navegação e Exploração

| Comando | Descrição |
| :--- | :--- |
| `pwd` | Mostra o caminho completo do diretório onde você está agora. |
| `ls` | Lista os arquivos e pastas do diretório atual. |
| `ls -la` | Lista tudo, incluindo arquivos ocultos, com detalhes de tamanho e permissões. |
| `cd <caminho>` | Entra em uma pasta. Ex: `cd /etc/nginx`. |
| `cd ..` | Volta um nível para cima na árvore de diretórios. |
| `cd ~` | Volta direto para a sua pasta pessoal (/home/usuario). |

---

## 2. Manipulação de Arquivos e Pastas

| Comando | Descrição |
| :--- | :--- |
| `mkdir <nome>` | Cria um novo diretório. |
| `touch <arquivo>` | Cria um arquivo vazio. |
| `cp <origem> <destino>` | Copia arquivos ou pastas. |
| `mv <origem> <destino>` | Move ou **renomeia** arquivos e pastas. |
| `rm <arquivo>` | Remove um arquivo. |
| `rm -rf <pasta>` | **Cuidado:** Remove uma pasta e todo o seu conteúdo recursivamente e à força. |

---

## 3. Atualização do Sistema (Ubuntu/Debian)

Manter o sistema atualizado é a primeira regra de segurança.

*   **Atualizar a lista de repositórios:**
    `sudo apt update` (Verifica se há versões novas dos programas).
*   **Instalar as atualizações:**
    `sudo apt upgrade` (Baixa e instala as novidades).
*   **Remover lixo/pacotes inúteis:**
    `sudo apt autoremove`.

---

## 4. Gerenciamento de Serviços (`systemctl`)

No Linux moderno (Systemd), usamos o `systemctl` para gerenciar programas que rodam em segundo plano (como Docker, Nginx ou Bancos de Dados).

*   **Subir um serviço:** `sudo systemctl start <serviço>`
*   **Descer (Parar) um serviço:** `sudo systemctl stop <serviço>`
*   **Reiniciar:** `sudo systemctl restart <serviço>`
*   **Verificar status:** `systemctl status <serviço>`
*   **Habilitar no boot:** `sudo systemctl enable <serviço>` (Faz o programa ligar junto com o PC).

---

## 5. Comandos Avançados e Kernel

### Atualizar o Kernel
Em distribuições como o Ubuntu, o Kernel é atualizado junto com o sistema, mas você pode forçar a busca por uma versão específica ou limpar versões antigas:
*   **Ver versão atual:** `uname -r`
*   **Atualizar tudo (incluindo Kernel):** `sudo apt full-upgrade`
*   **Instalar um Kernel específico:** `sudo apt install linux-image-<versão>`

### Monitoramento e Rede
*   **Ver consumo em tempo real:** `top` ou `htop` (mais visual).
*   **Ver uso de disco:** `df -h`.
*   **Ver endereços IP:** `ip addr` ou `ifconfig`.
*   **Testar conexão:** `ping <site/ip>`.

---

## 💡 Dica: O Poder do `sudo`
O comando `sudo` (SuperUser Do) permite que você execute comandos com privilégios de administrador (**root**). Use-o apenas quando necessário (instalações, configurações de sistema ou serviços).

---
**Links Relacionados:**
- [[Linux]] (Início)
- [[Arquitetura de Diretórios]]
- [[Troubleshooting no Linux]]
