# Guia Prático de Implementação de RAG

Este guia detalha os passos técnicos e as ferramentas necessárias para construir um sistema de **RAG (Retrieval-Augmented Generation)** funcional.

---

## 1. As Ferramentas Escolhidas (Stack Recomendada)

Para começar rapidamente com ferramentas de nível profissional:

*   **Linguagem:** Python (O ecossistema de IA é 90% Python).
*   **Orquestração:** **LangChain** ou **LlamaIndex**.
*   **Banco Vetorial Local:** **ChromaDB** (Fácil de instalar, não precisa de nuvem).
*   **Modelos de Embedding:** `text-embedding-3-small` (OpenAI) ou `all-MiniLM-L6-v2` (HuggingFace - roda local).
*   **LLM:** GPT-4o, Claude 3.5 Sonnet ou **Gemini 1.5 Pro**.

---

## 2. Passo a Passo da Execução

### Passo 1: Preparação e Ingestão
Você precisa transformar seus arquivos (PDF, TXT) em dados que o computador entenda.
```python
from langchain_community.document_loaders import PyPDFLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter

# Carrega o PDF
loader = PyPDFLoader("seu_documento.pdf")
data = loader.load()

# Divide em pedaços (Chunks)
# chunk_size: tamanho do pedaço / chunk_overlap: contexto repetido entre pedaços
text_splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=100)
chunks = text_splitter.split_documents(data)
```

### Passo 2: Criação do Banco Vetorial
Nesta etapa, o texto vira números (vetores) e é salvo no banco.
```python
from langchain_openai import OpenAIEmbeddings
from langchain_community.vectorstores import Chroma

# Cria o banco e salva os dados localmente na pasta 'db_storage'
vector_db = Chroma.from_documents(
    documents=chunks,
    embedding=OpenAIEmbeddings(),
    persist_directory="./db_storage"
)
```

### Passo 3: Execução da Consulta (Query)
O sistema busca a informação e envia para o LLM.
```python
from langchain.chains import RetrievalQA
from langchain_openai import ChatOpenAI

# Configura o LLM e a corrente de busca
llm = ChatOpenAI(model_name="gpt-4o")
qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=vector_db.as_retriever()
)

# Faz a pergunta
resposta = qa_chain.invoke("Qual o resumo do capítulo 2?")
print(resposta["result"])
```

---

## 3. Como Melhorar a Performance (RAG Avançado)

Se as respostas estiverem ruins, tente estas técnicas:

1.  **Hybrid Search (Busca Híbrida):** Combina a busca vetorial (semântica) com a busca por palavras-chave tradicional (BM25).
2.  **Re-ranking:** O sistema recupera 10 parágrafos, e um modelo menor (como o Cohere ReRank) reordena para garantir que o mais relevante seja o primeiro.
3.  **Contextual Compression:** O sistema resume os parágrafos encontrados antes de enviar para o LLM, removendo "ruído" e economizando tokens.
4.  **Metadata Filtering:** Adicione metadados (data, autor, categoria) aos seus chunks para filtrar a busca (ex: "Busque apenas em documentos de 2024").

---

## 4. Ferramentas Prontas para Uso (No-Code/Low-Code)

Se você não quer escrever código do zero:
*   **AnythingLLM:** Uma interface desktop que permite fazer RAG apenas arrastando arquivos (usa Docker por baixo).
*   **Dify.ai:** Plataforma open-source poderosa para criar fluxos de agentes e RAG visualmente.
*   **Verba (pela Weaviate):** Uma aplicação pronta focada 100% em RAG fácil de usar.

---
**Links Relacionados:**
- [[RAG (Retrieval-Augmented Generation)]] (Conceitos)
- [[Docker]] (Para rodar ChromaDB ou Dify localmente)
- [[Agentes e Ferramentas]]
