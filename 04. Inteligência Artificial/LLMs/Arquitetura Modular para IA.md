# Arquitetura Modular para Aplicações de IA

Construir aplicações de IA modulares significa aplicar os princípios de [[Clean Architecture]] para que o seu sistema não fique "preso" a um modelo específico (OpenAI, Anthropic, Gemini) ou a um banco de dados vetorial específico.

---

## 1. A Estrutura de Camadas (Padrão)

Para garantir a modularidade, dividimos a aplicação assim:

*   **Domain (Núcleo):** Define as interfaces e contratos. O que é um "Chat", o que é um "Documento", e as interfaces como `ILLMService` ou `IVectorDatabase`.
*   **Application (Casos de Uso):** Contém a lógica de orquestração. Ex: `RealizarConsultaRAG`, `ResumirDocumento`. Ela chama as interfaces sem saber quem as implementa.
*   **Infrastructure (Implementação):** Onde o código real toca as APIs externas. Ex: `OpenAIService`, `GeminiService`, `ChromaDBRepository`.
*   **Interface (API/CLI):** Onde a aplicação é exposta para o usuário.

---

## 2. Exemplo Prático de Organização de Pastas

```text
meu-projeto-ia/
├── src/
│   ├── domain/
│   │   ├── entities/          # Classes puras (Mensagem, Contexto)
│   │   └── interfaces/        # Contratos (ILLMProvider, IEmbeddingService)
│   ├── application/
│   │   ├── use_cases/         # Lógica RAG, Cadeias de Pensamento
│   │   └── dtos/              # Formatos de entrada e saída
│   └── infrastructure/
│       ├── llm_providers/     # Implementações (OpenAI, Gemini, Ollama)
│       ├── vector_store/      # Implementações (Chroma, Pinecone)
│       └── document_loaders/  # Leitores de PDF, Web, Notion
└── main.py                    # Injeção de Dependência (Onde tudo se une)
```

---

## 3. O Segredo da Modularidade: Inversão de Dependência

Se você usar o código abaixo no seu Caso de Uso, ele nunca precisará ser alterado se você trocar de IA:

```python
# domain/interfaces.py
class ILLMProvider(ABC):
    @abstractmethod
    def generate_response(self, prompt: str) -> str:
        pass

# application/use_cases.py
class ChatConsultant:
    def __init__(self, llm: ILLMProvider): # Depende da interface, não da classe real
        self.llm = llm

    def ask(self, user_query: str):
        # Lógica de negócio aqui
        return self.llm.generate_response(user_query)
```

---

## 4. Benefícios de ser Modular em IA

1.  **Troca de Modelos (Model Agnostic):** Se o Gemini 1.5 Pro ficar mais barato/rápido que o GPT-4o amanhã, você só muda uma linha na camada de infraestrutura.
2.  **Facilidade de Testes:** Você pode criar um `MockLLM` que não gasta dinheiro nem precisa de internet para testar a lógica do seu sistema.
3.  **Hospedagem Híbrida:** Você pode rodar um modelo pesado na nuvem (OpenAI) para tarefas complexas e um modelo leve local (Llama-3 via Ollama) para tarefas simples, usando a mesma estrutura de código.
4.  **Escalabilidade:** Novas ferramentas (como uma nova busca na web ou leitor de planilhas) entram como novos "Plugins" na camada de infraestrutura.

---
**Links Relacionados:**
- [[Clean Architecture]] (Conceitos base)
- [[LLMs]]
- [[Agentes e Ferramentas]] (Como os agentes se tornam plugins modulares)
