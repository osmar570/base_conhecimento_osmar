# Hospedando IAs Locais com Docker

Hospedar seus próprios modelos de linguagem (LLMs) localmente garante **privacidade total**, custo zero por token e a capacidade de trabalhar sem internet. O Docker é a ferramenta ideal para isso, pois isola as dependências complexas de drivers de GPU e bibliotecas de IA.

---

## 1. A Ferramenta Recomendada: Ollama

O **Ollama** é a forma mais simples de rodar modelos como Llama 3, Mistral e Gemma localmente.

### Rodando via Docker (Com aceleração de GPU NVIDIA)

```bash
docker run -d \
  --gpus=all \
  -v ollama:/root/.ollama \
  -p 11434:11434 \
  --name ollama \
  ollama/ollama
```

### Como baixar e usar um modelo:
Após subir o container, você "baixa" o modelo para dentro dele:
```bash
docker exec -it ollama ollama run llama3
```

---

## 2. Interface Visual: Open WebUI

Para ter uma experiência similar ao ChatGPT no seu navegador, você pode rodar o **Open WebUI** conectado ao seu container do Ollama.

### Docker Compose Sugerido:
```yaml
services:
  ollama:
    image: ollama/ollama:latest
    container_name: ollama
    volumes:
      - ollama_data:/root/.ollama
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]

  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    container_name: open-webui
    ports:
      - "3000:8080"
    environment:
      - OLLAMA_BASE_URL=http://ollama:11434
    depends_on:
      - ollama
    volumes:
      - webui_data:/app/backend/data

volumes:
  ollama_data:
  webui_data:
```

---

## 3. Outras Ferramentas Populares

*   **LocalAI:** Um substituto "drop-in" para a API da OpenAI. Ele emula os mesmos endpoints da OpenAI, permitindo que você use qualquer ferramenta compatível com GPT-4 apontando para o seu servidor local.
*   **vLLM:** Focado em alta performance e throughput. Ideal se você pretende servir múltiplos usuários simultaneamente a partir de uma única GPU potente.

---

## 4. Requisitos de Hardware

Para uma boa experiência local, os limites costumam ser a **VRAM** da sua placa de vídeo:

| Tamanho do Modelo | RAM/VRAM Mínima | Recomendado |
| :--- | :--- | :--- |
| **7B (Mistral/Llama)** | 8 GB | RTX 3060/4060 ou Apple M-Series |
| **13B/14B (Gemma/Qwen)** | 16 GB | RTX 3090/4090 |
| **70B (Llama 3 Large)** | 48 GB+ | 2x RTX 3090/4090 ou A100 |

---

## 5. Por que usar Docker para isso?

1.  **Drivers Isolados:** Evita conflitos de versões de CUDA e Python no seu sistema host.
2.  **Portabilidade:** Você pode configurar o ambiente no seu PC e movê-lo para um servidor na nuvem (como um `g2-standard` do GCP) em segundos.
3.  **Segurança:** O modelo e seus dados ficam restritos ao container, sem acesso aos seus arquivos pessoais, a menos que você mapeie um volume explicitamente.

---
**Links Relacionados:**
- [[Docker]] (Comandos básicos)
- [[LLMs]] (Índice de IA)
- [[RAG (Retrieval-Augmented Generation)]] (Conectando sua IA local aos seus dados)
