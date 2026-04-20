# Arquitetura de Diretórios (File Hierarchy Standard)

No Linux, tudo começa na **Raiz**, representada por uma barra (`/`). Todos os arquivos, pastas e até mesmo dispositivos de hardware (discos, teclados) são acessados como se fossem caminhos dentro desta árvore.

---

## 📂 Os Principais Diretórios

### `/bin` e `/sbin`
*   **`/bin`**: Contém comandos essenciais do sistema usados por todos os usuários (ex: `ls`, `cp`, `mkdir`).
*   **`/sbin`**: Contém binários do sistema para administração (geralmente executados pelo `root`).

### `/etc` (O Coração da Configuração)
Aqui ficam quase todos os arquivos de configuração do sistema e dos serviços instalados (ex: configurações de rede, senhas de sistema, configs do Apache/Nginx).

### `/home`
Pastas pessoais dos usuários comuns. Se o seu usuário é `osmar`, seus documentos estarão em `/home/osmar`.

### `/root`
O diretório pessoal do usuário administrador (Superusuário). Ele não fica em `/home/root`, mas sim na própria raiz por motivos de segurança.

### `/var` (Arquivos Variáveis)
Contém arquivos que mudam constantemente durante o uso do sistema.
*   **`/var/log`**: Onde ficam os logs do sistema (essencial para troubleshooting).
*   **`/var/www`**: Local padrão para arquivos de sites.
*   **`/var/lib/docker`**: Local onde o Docker armazena as imagens e containers.

### `/tmp`
Arquivos temporários. Geralmente são apagados toda vez que o computador é reiniciado.

### `/usr` (User Programs)
Onde ficam a maioria dos programas instalados pelo usuário e bibliotecas compartilhadas.
*   **`/usr/bin`**: Comandos menos essenciais.
*   **`/usr/share`**: Documentação e arquivos de ícones/fontes.

### `/opt` (Optional)
Reservado para a instalação de softwares de terceiros que não seguem o padrão da distribuição (ex: Google Chrome, pacotes proprietários).

### `/proc` e `/sys` (Sistemas Virtuais)
Estes não existem no disco físico! São diretórios criados na memória RAM pelo Kernel para você visualizar informações do hardware e processos em tempo real.

### `/dev` (Devices)
Contém arquivos que representam o hardware. No Linux, um disco rígido pode ser o arquivo `/dev/sda`.

---

## 💡 Dica de Ouro para DevOps
Como Engenheiro de Software ou DevOps, você passará 90% do seu tempo nestes três:
1.  **`/etc`**: Para configurar serviços.
2.  **`/var/log`**: Para descobrir por que algo quebrou.
3.  **`/home`**: Para desenvolver seu código.

---
**Links Relacionados:**
- [[Linux]] (Voltar para o Índice)
- [[Comandos Essenciais de Terminal]]
- [[Troubleshooting no Linux]]
