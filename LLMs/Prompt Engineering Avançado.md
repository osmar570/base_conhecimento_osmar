# Prompt Engineering Avançado

O **Prompt Engineering** é a disciplina de otimizar a entrada (input) para guiar o LLM a gerar resultados mais precisos, lógicos e úteis. Em nível avançado, deixamos de apenas "pedir coisas" e passamos a estruturar o fluxo de pensamento do modelo.

---

## 1. Técnicas de Raciocínio (Reasoning)

### A. Chain-of-Thought (Cadeia de Pensamento)
Força o modelo a detalhar o passo a passo lógico antes de dar a resposta final.
*   **Prompt:** *"Pense passo a passo para resolver este problema matemático: [Problema]. Explique seu raciocínio em cada etapa."*
*   **Por que funciona:** Reduz erros de cálculo e lógica ao permitir que o modelo use sua própria saída intermediária como contexto.

### B. Few-Shot Prompting
Fornece exemplos de entrada e saída para que o modelo aprenda o padrão esperado.
*   **Exemplo:**
    *"Entrada: O filme foi incrível! -> Sentimento: Positivo
    Entrada: Detestei o serviço. -> Sentimento: Negativo
    Entrada: O dia está nublado. -> Sentimento:"*
*   **Por que funciona:** Alinha o formato e o tom da resposta sem precisar de fine-tuning.

### C. Self-Criticism / Deliberation (Auto-Crítica)
Pede para o modelo revisar sua própria resposta.
*   **Fluxo:**
    1. Gere uma resposta para [X].
    2. Agora, identifique falhas ou imprecisões na resposta anterior.
    3. Escreva uma versão final melhorada com base na sua crítica.

---

## 2. Estruturação Técnica do Prompt (Frameworks)

Um prompt profissional deve ser estruturado. O framework **CO-STAR** é um dos mais eficazes:

*   **Context (Contexto):** Quem é o modelo? O que está acontecendo?
*   **Objective (Objetivo):** O que exatamente você quer que ele faça?
*   **Style (Estilo):** Qual o tom? (Executivo, engraçado, acadêmico).
*   **Tone (Tom):** Qual o sentimento? (Encorajador, neutro, urgente).
*   **Audience (Público):** Para quem é a resposta? (Um CEO, uma criança de 5 anos).
*   **Response (Resposta):** Qual o formato? (Markdown, JSON, Tabela).

---

## 3. Parâmetros de Controle (API)

Se você estiver usando o LLM via código (API), estes parâmetros mudam drasticamente o resultado:

*   **Temperature (Temperatura):** 
    *   `0.1 - 0.3`: Respostas focadas, determinísticas (Ideal para extração de dados).
    *   `0.7 - 1.0`: Respostas criativas, variadas (Ideal para escrita criativa).
*   **Top-P (Nucleus Sampling):** Filtra os tokens mais prováveis até somarem uma probabilidade P. Ajuda a manter a coerência.
*   **System Prompt:** Instruções de alto nível que definem o comportamento "base" do modelo (ex: "Você é um especialista em segurança cibernética que nunca fornece código malicioso").

---

## 4. Dicas para Melhorar a Performance

1.  **Seja Específico:** Evite "Escreva um código". Use "Escreva uma função em Python usando a biblioteca Pandas para limpar esta tabela CSV".
2.  **Use Delimitadores:** Use `---`, `###` ou `XML tags` para separar instruções de dados de exemplo.
3.  **Defina o Formato de Saída:** "Sua resposta deve ser estritamente um objeto JSON válido".
4.  **Dê uma "Saída de Emergência":** Instrua o modelo a dizer "Eu não sei" se ele não tiver certeza, reduzindo a [[LLMs#2. Conceitos Fundamentais|Alucinação]].

---
**Links Relacionados:**
- [[LLMs]]
- [[Fundamentos de GenAI]]
- [[RAG (Retrieval-Augmented Generation)]]
