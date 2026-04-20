# Git e Boas Práticas

## 1. O que é o Git?

O **Git** é o sistema de **Controle de Versão Distribuído (DVCS)** mais popular do mundo. Diferente de sistemas antigos, no Git cada desenvolvedor tem uma cópia completa de todo o histórico do projeto em sua própria máquina, o que o torna extremamente rápido e resiliente a falhas de rede.

Foi criado por **Linus Torvalds** (o mesmo criador do Linux) para gerenciar o desenvolvimento do kernel do Linux, o que explica seu foco em performance, integridade de dados e suporte a fluxos de trabalho complexos e paralelos.

## 2. Para que serve o Git?

O Git resolve problemas críticos no desenvolvimento de software:

*   **Histórico e Recuperação:** Permite viajar no tempo. Se você introduzir um bug hoje, pode ver exatamente o que mudou e reverter para uma versão que funcionava segundos antes.
*   **Trabalho em Equipe (Colaboração):** Permite que 10 ou 100 desenvolvedores trabalhem nos mesmos arquivos simultaneamente sem sobrescrever o trabalho um do outro, através do sistema de **Merge** e **Pull Requests**.
*   **Ramificação (Branching):** Você pode criar uma "ramificação" para testar uma nova ideia ou corrigir um bug sem afetar o código principal (branch `main`). Se a ideia funcionar, você a integra de volta; se não, basta deletar a branch.
*   **Auditabilidade:** Em ambientes profissionais, o Git diz exatamente **QUEM** mudou **O QUÊ** e **QUANDO**. Isso é vital para segurança e compliance.
*   **Backup Nativo:** Como o Git é distribuído, se o servidor central (como o GitHub) cair, cada desenvolvedor ainda possui o projeto inteiro com todo o histórico salvo localmente.

## 🗺️ Trilha de Aprendizagem

1.  **Conventional Commits:** Entender a especificação para mensagens de commit.
    *   [[Conventional Commits e Commit Lint]]
2.  **Git Flow vs GitHub Flow:** Estratégias de ramificação (branches).
3.  **Hooks do Git:** Como automatizar tarefas antes de um commit ou push (Husky).

---
**Links Relacionados:**
- [[Clean Architecture]] (Para manter o código tão limpo quanto o histórico)
- [[Linux/Shell Scripting e Automação]] (Muitos hooks de Git são scripts .sh)
