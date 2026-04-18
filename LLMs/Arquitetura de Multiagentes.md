# Arquitetura de Multiagentes

A **Arquitetura de Multiagentes** é um paradigma onde múltiplos LLMs (agentes) com perfis, memórias e ferramentas diferentes trabalham juntos para resolver um problema que seria complexo demais para um único modelo. É como passar de um "trabalhador autônomo" para uma "empresa completa".

---

## 1. Por que usar Multiagentes?

Um único LLM, por mais potente que seja, tem limites de foco e raciocínio. Ao usar múltiplos agentes, você ganha:

*   **Especialização:** Cada agente é um mestre em sua área (ex: um Codificador, um Revisor e um Testador).
*   **Redução de Erros:** Agentes podem revisar o trabalho uns dos outros (Self-Correction).
*   **Modularidade:** É mais fácil dar ferramentas específicas para cada agente em vez de dar 50 ferramentas para um só.
*   **Paralelismo:** Diferentes partes de um projeto podem ser feitas simultaneamente.

---

## 2. Conceitos Chave

1.  **Role (Papel):** Define a especialidade do agente (ex: "Analista de Segurança").
2.  **Backstory (Contexto):** Dá profundidade à personalidade do agente, influenciando o tom e o rigor.
3.  **Processo (Orquestração):** Como os agentes conversam?
    *   **Sequencial:** Agente A termina e passa para o Agente B.
    *   **Hierárquico:** Um agente "Gerente" coordena e delega para os outros.
    *   **Consenso:** Todos discutem até chegar a uma solução.

---

## 3. Principais Frameworks

*   **CrewAI:** Focado em processos e "vibe" de equipe. Muito fácil de começar.
*   **Microsoft AutoGen:** Extremamente potente para agentes que conversam de forma autônoma e executam código.
*   **LangGraph (LangChain):** Oferece o maior controle sobre o fluxo, tratando agentes como nós em um gráfico (grafo).

---

## 4. Exemplo Prático (Python + CrewAI)

Vamos criar uma equipe para **Pesquisa e Redação Técnica**.

```python
from crewai import Agent, Task, Crew, Process

# 1. Definindo os Agentes
pesquisador = Agent(
  role='Pesquisador de Tecnologias',
  goal='Encontrar as 3 maiores tendências em Kubernetes para 2024',
  backstory='Você é um analista experiente focado em infraestrutura cloud-native.',
  allow_delegation=False,
  verbose=True
)

escritor = Agent(
  role='Redator Técnico',
  goal='Escrever um post de blog amigável sobre as tendências encontradas',
  backstory='Você transforma conceitos técnicos complexos em textos simples e atraentes.',
  allow_delegation=False,
  verbose=True
)

# 2. Definindo as Tarefas
tarefa_pesquisa = Task(description='Pesquise sobre as novidades do K8s.', agent=pesquisador)
tarefa_escrita = Task(description='Crie o post com base na pesquisa.', agent=escritor)

# 3. Criando a Equipe (Crew)
equipe = Crew(
  agents=[pesquisador, escritor],
  tasks=[tarefa_pesquisa, tarefa_escrita],
  process=Process.sequential # O escritor espera o pesquisador terminar
)

resultado = equipe.start()
print(resultado)
```

---

## 5. Como Começar (Passo a Passo)

1.  **Identifique os Papéis:** Se você fosse contratar humanos para essa tarefa, quais seriam seus cargos?
2.  **Escolha as Ferramentas:** O pesquisador precisa de busca na web. O escritor precisa apenas do resultado da pesquisa.
3.  **Defina o Fluxo:** É uma linha de produção (Sequencial) ou precisa de um gerente (Hierárquico)?
4.  **Teste e Refine:** Se o escritor está sendo técnico demais, ajuste o `backstory` dele para ser mais didático.

---
**Links Relacionados:**
- [[Agentes e Ferramentas]] (Conceito de agente único)
- [[LLMs]] (Índice de IA)
- [[Prompt Engineering Avançado]] (Para escrever os Backstories)
