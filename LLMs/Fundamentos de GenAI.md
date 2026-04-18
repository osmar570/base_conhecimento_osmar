# Fundamentos de GenAI (Generative AI)

A Inteligência Artificial Generativa moderna é impulsionada por avanços em redes neurais que permitem não apenas classificar dados, mas criar novos conteúdos originais. O divisor de águas nessa área foi o surgimento da arquitetura **Transformer**.

## 1. A Revolução do Transformer

Antes de 2017, o processamento de linguagem usava redes que liam palavras uma por uma (RNNs). O paper *"Attention Is All You Need"* mudou tudo ao introduzir o **Transformer**, que permite processar frases inteiras de uma vez, capturando relações de longa distância entre palavras.

### Componentes Principais:
*   **Encoder (Codificador):** Lê e compreende o texto de entrada (transforma palavras em vetores matemáticos).
*   **Decoder (Decodificador):** Gera o texto de saída, prevendo o próximo token com base no que foi compreendido.
*   **Embeddings:** Representações numéricas de palavras onde termos com significados próximos ficam "perto" geometricamente.

## 2. O Mecanismo de Atenção (Self-Attention)

O "segredo" do sucesso dos LLMs é a capacidade de dar pesos diferentes para partes diferentes da entrada.
*   **Exemplo:** Na frase *"O animal não atravessou a rua porque **ele** estava cansado"*, o mecanismo de atenção ajuda o modelo a entender que o token **"ele"** refere-se ao **"animal"** e não à "rua".

## 3. O Processo de Treinamento

Um LLM passa por fases distintas até chegar ao usuário:

1.  **Pre-training (Pré-treinamento):** O modelo lê trilhões de palavras da internet para aprender gramática, fatos e raciocínio básico. É aqui que ele se torna "Large".
2.  **Fine-tuning (Ajuste Fino):** O modelo é treinado em dados específicos (como diálogos ou código) para aprender a seguir instruções.
3.  **RLHF (Reinforcement Learning from Human Feedback):** Humanos avaliam as respostas do modelo, ensinando-o a ser mais útil, seguro e menos propenso a gerar conteúdo tóxico.

## 4. Probabilidade e Próximo Token

No fundo, um LLM é um preditor estatístico altamente sofisticado. Ele não "sabe" fatos como um banco de dados; ele calcula qual é o **próximo token mais provável** dada a sequência anterior.

---
**Links Relacionados:**
- [[LLMs]] (Voltar para o Índice)
- [[Prompt Engineering Avançado]]
- [[RAG (Retrieval-Augmented Generation)]]
