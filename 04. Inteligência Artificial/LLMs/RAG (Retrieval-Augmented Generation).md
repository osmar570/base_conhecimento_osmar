# RAG (Retrieval-Augmented Generation)

O **RAG** é uma técnica que permite a um LLM acessar informações externas e atualizadas que não faziam parte do seu conjunto de dados original de treinamento. É como dar ao modelo um **"livro de consulta"** ou acesso a uma biblioteca em tempo real.

---

## 1. Por que o RAG é necessário?

Os LLMs possuem dois problemas principais que o RAG resolve:
1.  **Data Cutoff (Data de Corte):** O modelo só sabe o que aconteceu até o dia em que terminou seu treinamento.
2.  **Hallucination (Alucinação):** O modelo pode inventar fatos sobre assuntos que não conhece.
3.  **Privacidade:** Você não quer enviar seus dados confidenciais para treinar o GPT-4, mas quer que o GPT-4 responda perguntas sobre eles.

---

## 2. Como o RAG funciona (O Fluxo)

O processo de RAG segue 4 passos fundamentais:

1.  **Ingestão:** Seus documentos (PDFs, Markdown, Tabelas) são quebrados em pequenos pedaços (*chunks*).
2.  **Embedding:** Cada pedaço é transformado em um vetor numérico (usando um modelo de embedding).
3.  **Armazenamento:** Esses vetores são guardados em um **Vector Database** (Banco de Dados Vetorial).
4.  **Recuperação (Retrieval):** Quando o usuário faz uma pergunta, o sistema busca no banco os pedaços de texto mais "próximos" (semanticamente similares) à pergunta e os envia para o LLM como contexto.

---

## 3. Como Começar a Fazer RAG

Para construir seu primeiro sistema de RAG, você precisará desta "stack" básica:

### A. Ferramentas de Orquestração (O "Cérebro")
*   **LangChain:** A biblioteca mais popular para conectar LLMs a fontes de dados.
*   **LlamaIndex:** Especializada em indexação e busca de dados para LLMs.

### B. Banco de Dados Vetoriais (A "Memória")
*   **ChromaDB:** Excelente para começar (roda localmente).
*   **Pinecone:** Solução em nuvem (SaaS) altamente escalável.
*   **FAISS:** Biblioteca do Meta para busca vetorial rápida.

### C. Estratégia de Implementação (Passo a Passo)

1.  **Carga de Dados:** Use um `PDFLoader` para ler seus manuais ou documentos.
2.  **Chunking:** Divida o texto (ex: pedaços de 500 caracteres com sobreposição de 50).
3.  **Vetorização:** Use a API da OpenAI (`text-embedding-3-small`) ou modelos locais como `HuggingFaceEmbeddings`.
4.  **Query:** Quando o usuário perguntar: *"Qual a política de férias?"*:
    *   O sistema busca os parágrafos que falam de "férias".
    *   O prompt enviado ao LLM será: *"Com base nos parágrafos abaixo, responda à pergunta do usuário: [Parágrafos recuperados]"*.

---

## 4. Desafios do RAG

*   **Qualidade da Recuperação:** Se o sistema buscar o parágrafo errado, a resposta será errada.
*   **Tamanho do Contexto:** Enviar informação demais pode confundir o modelo ou ser caro (tokens).
*   **Chunking Strategy:** A forma como você corta o texto muda completamente o que o modelo "entende".

---
**Links Relacionados:**
- [[LLMs]]
- [[Prompt Engineering Avançado]] (Fundamental para criar o prompt do RAG)
- [[Clean Architecture]] (Para organizar o código do seu sistema de RAG)
