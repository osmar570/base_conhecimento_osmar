# Gestão de Usuários e Grupos no Linux

O Linux é um sistema multiusuário. Gerenciar identidades corretamente é a primeira linha de defesa para garantir a segurança e o isolamento de processos e dados.

---

## 1. Comandos de Gerenciamento

### Usuários
*   **`sudo useradd -m <nome>`**: Cria um novo usuário com pasta pessoal (`-m`).
*   **`sudo passwd <nome>`**: Define ou altera a senha do usuário.
*   **`sudo userdel -r <nome>`**: Remove o usuário e sua pasta pessoal (`-r`).
*   **`id <nome>`**: Mostra o UID (User ID) e os grupos aos quais o usuário pertence.

### Grupos
*   **`sudo groupadd <grupo>`**: Cria um novo grupo.
*   **`sudo usermod -aG <grupo> <usuario>`**: Adiciona um usuário a um grupo secundário (o `-a` é vital para não remover os grupos atuais).
*   **`getent group <grupo>`**: Lista todos os membros de um grupo específico.

---

## 2. O arquivo `/etc/sudoers`

O `sudo` permite que usuários comuns executem tarefas de root. Para dar esse poder a alguém, usamos o comando:
`sudo visudo`

*   **Regra de Ouro:** Nunca edite o arquivo `/etc/sudoers` diretamente com o `nano` ou `vim`. Use sempre o `visudo`, pois ele valida a sintaxe antes de salvar, evitando que você fique "trancado" fora do sistema.

---

## 3. Script de Automação: Criação de Usuários em Massa

Este script automatiza a criação de múltiplos usuários, define uma senha padrão (solicitada no início) e os adiciona a um grupo específico.

```bash
#!/bin/bash

# Script para criação automatizada de usuários
# Uso: ./criar_usuarios.sh user1 user2 user3

if [ $# -eq 0 ]; then
    echo "Erro: Forneça pelo menos um nome de usuário."
    echo "Exemplo: $0 joao maria osmar"
    exit 1
fi

echo -n "Digite a senha padrão para os novos usuários: "
read -s SENHA
echo

# Grupo padrão para novos membros
GRUPO_PADRAO="equipe_dev"
sudo groupadd -f $GRUPO_PADRAO

for USUARIO in "$@"; do
    if id "$USUARIO" &>/dev/null; then
        echo "Aviso: O usuário $USUARIO já existe. Pulando..."
    else
        # Cria usuário, pasta home e define shell padrão bash
        sudo useradd -m -s /bin/bash "$USUARIO"
        
        # Define a senha silenciosamente
        echo "$USUARIO:$SENHA" | sudo chpasswd
        
        # Adiciona ao grupo da equipe
        sudo usermod -aG $GRUPO_PADRAO "$USUARIO"
        
        echo "✅ Usuário $USUARIO criado e adicionado ao grupo $GRUPO_PADRAO."
    fi
done

echo "--------------------------------------------------"
echo "Processo concluído!"
```

---

## 4. Arquivos de Identidade do Sistema

*   **`/etc/passwd`**: Lista todos os usuários do sistema, shells e pastas home.
*   **`/etc/shadow`**: Armazena as senhas criptografadas (acessível apenas pelo root).
*   **`/etc/group`**: Lista todos os grupos e seus membros.

---

## 💡 Dica de Segurança: Desativação Temporária
Se um funcionário sair da empresa ou um usuário for suspeito, em vez de deletar (o que apaga os arquivos), você pode apenas bloquear o acesso:
`sudo usermod -L <nome>` (Lock - bloqueia a senha)
`sudo usermod -U <nome>` (Unlock - desbloqueia)

---
**Links Relacionados:**
- [[Linux]] (Início)
- [[Sistema de Permissões]] (rwx)
- [[Shell Scripting e Automação]]
