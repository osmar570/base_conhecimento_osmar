# Conventional Commits e Commit Lint

A especificação [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) é uma convenção leve sobre as mensagens de commit. Ela fornece um conjunto de regras para criar um histórico de commits explícito e fácil de ler.

---

## 1. Estrutura da Mensagem

A mensagem do commit deve ser estruturada da seguinte forma:

```text
<tipo>[escopo opcional]: <descrição>

[corpo opcional]

[rodapé(s) opcional(ais)]
```

### Exemplo:
`feat(auth): add google login integration`

---

## 2. Principais Tipos

*   **`feat`**: Uma nova funcionalidade para o usuário.
*   **`fix`**: Correção de um bug.
*   **`docs`**: Alterações apenas na documentação.
*   **`style`**: Alterações que não afetam o significado do código (espaço em branco, formatação, falta de ponto e vírgula, etc).
*   **`refactor`**: Uma alteração de código que não corrige um bug nem adiciona uma funcionalidade.
*   **`perf`**: Uma alteração de código que melhora o desempenho.
*   **`test`**: Adição de testes ausentes ou correção de testes existentes.
*   **`build`**: Alterações que afetam o sistema de build ou dependências externas (ex: npm, composer, maven).
*   **`ci`**: Alterações em arquivos e scripts de configuração de CI (ex: GitHub Actions, Jenkins).
*   **`chore`**: Outras alterações que não modificam arquivos de src ou de teste.
*   **`revert`**: Reverte um commit anterior.

---

## 3. Breaking Changes (Mudanças Quebrantes)

Indica que o commit introduz uma mudança que quebra a compatibilidade com versões anteriores. 
*   Representada por um `!` após o tipo/escopo ou por uma nota `BREAKING CHANGE:` no rodapé.
*   Exemplo: `feat(api)!: change user endpoint response structure`

---

## 4. O que é Commit Lint?

O **Commit Lint** é uma ferramenta que verifica se as suas mensagens de commit seguem a convenção definida. Se a mensagem não estiver no padrão, o commit é bloqueado.

### Como implementar (Node.js):
1.  **Instalar Commitlint:** 
    `npm install --save-dev @commitlint/config-conventional @commitlint/cli`
2.  **Configurar:** Criar um arquivo `commitlint.config.js`:
    `module.exports = { extends: ['@commitlint/config-conventional'] };`
3.  **Husky:** Usar o **Husky** para rodar o commitlint automaticamente no gatilho de `commit-msg` do Git.

---

## 5. Vantagens
1.  **Changelogs Automáticos:** Ferramentas podem ler os commits `feat` e `fix` para gerar notas de lançamento.
2.  **Semântica de Versão (SemVer):** Ajuda a decidir se a próxima versão deve ser Patch, Minor ou Major.
3.  **Busca Facilitada:** Mais fácil filtrar o histórico: `git log --grep="^feat"`

---
**Links Relacionados:**
- [[Git]] (Índice)
- [[Linux/Comandos Essenciais de Terminal]] (Uso básico de Git via CLI)
