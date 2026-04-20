# Agentes e Ferramentas (Sistemas Agentic)

Um **Agente** é um sistema onde o LLM atua como o "cérebro" que orquestra o uso de ferramentas (tools) para resolver problemas complexos. Diferente de um chatbot comum, um agente possui autonomia para planejar, executar ações e aprender com os erros.

---

## 1. O que compõe um Agente?

Um sistema agentic é geralmente composto por:
1.  **Perfil/Persona:** Define quem o agente é e qual sua especialidade (ex: "Você é um Engenheiro DevOps").
2.  **Planejamento:** A capacidade de quebrar uma tarefa grande em sub-tarefas menores.
3.  **Ferramentas (Tools):** Funções que o agente pode chamar (ex: pesquisar na web, ler arquivos, executar código shell).
4.  **Memória:** A capacidade de lembrar de interações passadas para manter o contexto.

---

## 2. Exemplo Prático: Gemini CLI

O **Gemini CLI** (este ambiente que estamos usando) é um exemplo real de sistema multi-agente.

### Como ele funciona:
Quando você faz uma pergunta complexa, o Agente Principal (Orquestrador) decide:
*   Se ele precisa pesquisar no código (`grep_search`).
*   Se ele precisa ler um arquivo (`read_file`).
*   Se ele deve delegar a tarefa para um **Sub-Agente** especializado (ex: `codebase_investigator` ou `cli_help`).

### Anatomia de um Agente no Gemini CLI:
Um agente aqui é definido por um conjunto de instruções (System Prompt) e um catálogo de ferramentas.

---

## 3. Como Criar e Usar Agentes

Existem duas formas principais de criar agentes hoje:

### A. Via Frameworks (LangChain / CrewAI)
Você define o agente no código Python/Node.js:
```python
# Exemplo conceitual (CrewAI)
pesquisador = Agent(
  role='Pesquisador Senior',
  goal='Encontrar vulnerabilidades no código',
  backstory='Especialista em segurança com 20 anos de experiência',
  tools=[search_tool, read_file_tool]
)
```

### B. Customizando o Gemini CLI (Sub-Agentes)
Você pode criar seus próprios especialistas dentro desta ferramenta.
*   **Ação:** Use o comando `/help` ou consulte o `cli_help` para ver como criar arquivos de configuração de agentes.
*   **Uso:** Uma vez criado, você o invoca pelo nome, e ele terá seu próprio contexto e ferramentas específicas.

---

## 4. O Ciclo de Vida do Agente (Loop ReAct)

A maioria dos agentes opera no ciclo **ReAct** (Reasoning + Acting):
1.  **Pensamento (Thought):** O que eu preciso fazer agora?
2.  **Ação (Action):** Qual ferramenta eu vou usar? (ex: `run_shell_command`).
3.  **Observação (Observation):** O que a ferramenta retornou?
4.  **(Repete):** O agente avalia se o objetivo foi atingido ou se precisa de mais uma ação.

---

## 5. Ferramentas (Tool Calling)

Para que um LLM use uma ferramenta, ele não "roda" o código. Ele retorna um JSON indicando **qual** função ele quer chamar e com quais **parâmetros**. O sistema (como o Gemini CLI) executa a função e devolve o resultado para o LLM.

---
**Links Relacionados:**
- [[LLMs]]
- [[Prompt Engineering Avançado]] (Essencial para criar a persona do agente)
- [[Clean Architecture]] (Para estruturar o código das ferramentas)
