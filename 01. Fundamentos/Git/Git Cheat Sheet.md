# Git Cheat Sheet (Comandos Essenciais)

Este guia reúne os comandos mais utilizados no Git, organizados por etapas do fluxo de trabalho.

---

## 1. Configuração Inicial

| Comando | Descrição |
| :--- | :--- |
| `git config --global user.name "Seu Nome"` | Define o nome que aparecerá nos commits. |
| `git config --global user.email "seu@email.com"` | Define o e-mail atrelado aos commits. |
| `git init` | Inicia um novo repositório Git na pasta atual. |
| `git clone <url>` | Baixa um repositório existente do servidor. |

---

## 2. Ciclo de Vida do Commit (Local)

| Comando | Descrição |
| :--- | :--- |
| `git status` | Mostra quais arquivos foram alterados, deletados ou novos. |
| `git add <arquivo>` | Adiciona um arquivo para a área de preparação (Stage). |
| `git add .` | Adiciona **todas** as alterações do diretório para o Stage. |
| `git commit -m "mensagem"` | Salva as alterações do Stage no histórico permanentemente. |
| `git commit --amend` | Adiciona alterações ao último commit (ou corrige a mensagem dele). |
| `git log` | Mostra o histórico de todos os commits realizados. |
| `git diff` | Mostra a diferença detalhada linha a linha do que mudou. |

---

## 3. Ramificações (Branches) e Reescrita

| Comando | Descrição |
| :--- | :--- |
| `git branch` | Lista todas as branches locais. |
| `git checkout -b <nome>` | Cria uma nova branch e já entra nela. |
| `git checkout <nome>` | Muda para uma branch existente. |
| `git merge <nome>` | Une as alterações da branch especificada na branch atual. |
| `git rebase <branch>` | Reaplica seus commits em cima da ponta de outra branch (histórico linear). |
| `git rebase -i HEAD~n` | **Rebase Interativo:** Abre um editor para fundir (squash), renomear ou deletar commits dos últimos "n" commits. |
| `git branch -d <nome>` | Deleta uma branch local. |

---

## 4. Sincronização (Remoto)

| Comando | Descrição |
| :--- | :--- |
| `git remote add origin <url>` | Conecta seu repositório local a um servidor remoto. |
| `git fetch` | Baixa as novidades do servidor, mas não altera seu código. |
| `git pull` | Baixa as novidades e já tenta fazer o merge no seu código. |
| `git push origin <branch>` | Envia seus commits locais para o servidor. |

---

## 5. Desfazendo Alterações (O "Painel de Emergência")

| Comando | Descrição |
| :--- | :--- |
| `git checkout -- <arquivo>` | Descarta as alterações não salvas de um arquivo. |
| `git reset HEAD <arquivo>` | Tira o arquivo da área de Stage (mas mantém o código). |
| `git reset --hard HEAD~1` | **Cuidado:** Apaga o último commit e descarta todo o código dele. |
| `git revert <hash>` | Cria um novo commit que desfaz exatamente o que o commit alvo fez. |

---

## 💡 Dica de Produtividade: Aliases
Você pode criar atalhos para comandos longos. Exemplo:
`git config --global alias.st status`
Agora basta digitar `git st`.

---
**Links Relacionados:**
- [[Git]] (Índice e Fundamentos)
- [[Conventional Commits e Commit Lint]] (Como escrever boas mensagens)
- [[Linux/Comandos Essenciais de Terminal]]
