# Sistema de Permissões (rwx)

O Linux é um sistema multiusuário, o que significa que ele precisa de um controle rigoroso sobre quem pode ler, escrever ou executar arquivos. Cada arquivo ou diretório possui um conjunto de permissões atrelado a três entidades.

---

## 1. As Três Entidades (Dono, Grupo, Outros)

Ao rodar um `ls -l`, você verá algo como `-rwxr-xr--`. Essas letras são divididas em 3 grupos:

1.  **User (u):** O dono do arquivo (quem o criou).
2.  **Group (g):** Usuários que pertencem ao grupo do arquivo.
3.  **Others (o):** Qualquer outro usuário do sistema.

---

## 2. O Significado de `r`, `w`, `x`

| Letra | Significado | Valor Octal | Ação em Arquivos | Ação em Pastas |
| :--- | :--- | :--- | :--- | :--- |
| **r** | Read (Leitura) | 4 | Ver o conteúdo | Listar arquivos da pasta |
| **w** | Write (Escrita) | 2 | Alterar o conteúdo | Criar/Deletar arquivos na pasta |
| **x** | Execute (Execução) | 1 | Rodar o arquivo (script/binário) | Entrar na pasta (`cd`) |

---

## 3. Alterando Permissões com `chmod`

Existem duas formas de usar o comando `chmod` (Change Mode):

### A. Modo Simbólico (Mais fácil de lembrar)
*   `chmod u+x arquivo`: Dá permissão de **execução** para o **usuário**.
*   `chmod g-w arquivo`: Remove permissão de **escrita** do **grupo**.
*   `chmod a+r arquivo`: Dá permissão de **leitura** para **todos** (all).

### B. Modo Octal (Mais rápido e profissional)
Soma-se os valores: `4 (r) + 2 (w) + 1 (x)`.
*   `chmod 777 arquivo`: Permissão total para todos (Perigoso!).
*   `chmod 755 pasta`: Dono faz tudo, outros apenas leem e entram na pasta (Padrão para pastas).
*   `chmod 644 arquivo`: Dono lê/escreve, outros apenas leem (Padrão para arquivos de texto).

---

## 4. Alterando Donos com `chown`

O comando `chown` (Change Owner) muda quem é o dono do arquivo ou a qual grupo ele pertence.

*   `sudo chown osmar arquivo.txt`: Muda o dono para o usuário `osmar`.
*   `sudo chown osmar:www-data arquivo.txt`: Muda o dono para `osmar` e o grupo para `www-data`.
*   `sudo chown -R osmar:osmar /minha/pasta`: Muda o dono de **toda a pasta e subpastas** recursivamente.

---

## 5. Permissões Especiais

*   **SUID:** Permite que um arquivo seja executado com os privilégios do dono (ex: o comando `passwd`).
*   **Sticky Bit:** Usado em pastas como `/tmp`. Permite que todos criem arquivos, mas apenas o dono do arquivo pode deletá-lo.

---

## 💡 Dica de Troubleshooting
Se você receber um erro de "Permission Denied" tentando rodar um script que você acabou de criar:
`chmod +x seu_script.sh`

Se o Docker não conseguir ler um volume mapeado:
`sudo chown -R 1000:1000 /caminho/do/volume` (Geralmente o UID 1000 é o seu usuário padrão).

---
**Links Relacionados:**
- [[Linux]]
- [[Comandos Essenciais de Terminal]]
- [[Shell Scripting e Automação]] (Onde o +x é indispensável)
