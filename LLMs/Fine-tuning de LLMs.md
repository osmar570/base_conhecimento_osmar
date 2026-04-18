# Fine-tuning de LLMs

O **Fine-tuning** (Ajuste Fino) é o processo de pegar um modelo já treinado (como Llama 3, Mistral ou GPT-2) e treiná-lo um pouco mais em um conjunto de dados específico e menor. Isso permite que o modelo aprenda um estilo, tom ou domínio de conhecimento muito específico.

---

## 1. Fine-tuning vs. RAG: Qual escolher?

Esta é a dúvida mais comum. Use esta tabela para decidir:

| Característica | RAG (Consulta) | Fine-tuning (Treino) |
| :--- | :--- | :--- |
| **Conhecimento Externo** | Excelente (acessa novos fatos) | Ruim (fatos ficam defasados) |
| **Estilo/Tom/Formato** | Médio (via prompt) | Excelente (aprende o padrão) |
| **Alucinação** | Reduzida (baseada em fatos) | Pode aumentar se mal treinado |
| **Custo/Complexidade** | Baixo | Alto (exige GPU e dados limpos) |
| **Latência** | Maior (devido à busca) | Menor (está no "cérebro" do modelo) |

**Resumo:** Use **RAG** para fatos e documentos. Use **Fine-tuning** para comportamento, tom e domínios ultra-específicos (ex: diagnósticos médicos ou código proprietário).

---

## 2. Técnicas Modernas: PEFT e LoRA

Antigamente, o fine-tuning exigia supercomputadores para atualizar todos os bilhões de parâmetros. Hoje usamos o **PEFT (Parameter-Efficient Fine-Tuning)**.

### LoRA (Low-Rank Adaptation)
Em vez de mudar o modelo inteiro, o LoRA adiciona pequenas "camadas adaptadoras" ao lado das originais. Você treina apenas essas camadas minúsculas.
*   **Vantagem:** Reduz o uso de memória em 10.000x. Você consegue treinar modelos potentes em GPUs domésticas (como uma RTX 3090/4090).

---

## 3. Exemplo Prático (Python + Hugging Face)

A biblioteca `trl` e o `SFTTrainer` (Supervised Fine-tuning Trainer) são os padrões atuais.

```python
from trl import SFTTrainer
from transformers import AutoModelForCausalLM, AutoTokenizer, TrainingArguments
from datasets import load_dataset

# 1. Carregar o Modelo e Tokenizer (ex: Mistral-7B)
model_name = "mistralai/Mistral-7B-v0.1"
tokenizer = AutoTokenizer.from_pretrained(model_name)

# 2. Carregar seu conjunto de dados (deve ter o formato de instrução)
dataset = load_dataset("json", data_files="meus_dados_treino.jsonl", split="train")

# 3. Configurar Parâmetros de Treino
training_args = TrainingArguments(
    output_dir="./resultados",
    per_device_train_batch_size=4,
    learning_rate=2e-4,
    num_train_epochs=3,
    logging_steps=10,
)

# 4. Iniciar o Trainer (usando LoRA por baixo dos panos)
trainer = SFTTrainer(
    model=model_name,
    train_dataset=dataset,
    dataset_text_field="text", # Campo que contém o texto
    max_seq_length=512,
    args=training_args,
)

trainer.train()
```

---

## 4. Ferramentas para Facilitar a Vida

Se você não quer escrever todo o código de treino, use estas ferramentas:

*   **Unsloth:** Uma biblioteca que torna o fine-tuning do Llama e Mistral até 2x mais rápido e usa 70% menos memória.
*   **Axolotl:** Uma ferramenta baseada em configuração YAML. Você descreve o que quer no arquivo e ele faz o treino.
*   **Hugging Face AutoTrain:** Uma interface quase "no-code" para treinar modelos de forma simples.

## 5. Cuidados Importantes

1.  **Catastrophic Forgetting:** Se você treinar demais em um assunto, o modelo pode "esquecer" como falar ou raciocinar sobre outros temas.
2.  **Qualidade dos Dados:** "Lixo entra, lixo sai". Mil exemplos perfeitos valem mais que 100 mil exemplos com erros.

---
**Links Relacionados:**
- [[LLMs]]
- [[Fundamentos de GenAI]] (Fases de treinamento)
- [[RAG (Retrieval-Augmented Generation)]]
