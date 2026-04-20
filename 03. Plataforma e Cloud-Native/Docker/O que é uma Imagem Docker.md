# O que é uma Imagem Docker?

Uma **Imagem Docker** é um pacote executável, leve e autônomo que inclui tudo o que é necessário para executar uma aplicação: código, runtime, ferramentas do sistema, bibliotecas e configurações.

Se o [[O que são Containers (Detalhes Técnicos)|Contêiner]] é a instância em execução, a Imagem é o "molde" ou o "blueprint" (projeto).

## 1. Características Principais

*   **Imutabilidade (Read-Only):** Uma vez que uma imagem é construída, ela nunca muda. Se você precisar atualizar o código, você constrói uma nova imagem.
*   **Portabilidade:** Como a imagem contém todas as dependências, ela garante que a aplicação rode da mesma forma em qualquer lugar que tenha o Docker instalado.
*   **Composição por Camadas:** Imagens são construídas em cima de outras imagens, formando uma pilha de camadas.

## 2. A Estrutura de Camadas

As imagens utilizam um conceito chamado **Layering**. Cada comando em um script de criação gera uma nova camada no sistema de arquivos.

Exemplo de camadas:
1.  **Camada Base:** Geralmente um Sistema Operacional mínimo (ex: Alpine, Ubuntu).
2.  **Camada de Dependências:** Instalação de pacotes (ex: Python, Node.js).
3.  **Camada da Aplicação:** O código-fonte da sua aplicação.

Essas camadas são compartilhadas. Se você tem 5 imagens diferentes que usam o `Ubuntu` como base, o Docker baixa o Ubuntu apenas uma vez no seu disco, economizando muito espaço.

## 3. Como uma Imagem é Criada? (Dockerfile)

A "receita" para criar uma imagem é um arquivo de texto chamado **Dockerfile**. Ele contém instruções sequenciais:

```dockerfile
FROM node:18-alpine          # Imagem base
WORKDIR /app                 # Diretório de trabalho
COPY . .                     # Copia os arquivos locais para a imagem
RUN npm install              # Executa um comando na construção
CMD ["node", "server.js"]    # Comando executado quando o contêiner inicia
```

Ao rodar o comando `docker build`, o Docker processa esse arquivo e gera a imagem final.

## 4. Onde as Imagens ficam guardadas? (Registries)

Imagens são armazenadas e compartilhadas através de **Registries**.
*   **Docker Hub:** O registro público padrão onde empresas e a comunidade disponibilizam imagens oficiais (Nginx, MySQL, Python, etc).
*   **Registries Privados:** Empresas costumam usar o AWS ECR, Google Container Registry ou instâncias próprias do Docker Registry para guardar imagens confidenciais.

---
**Links Relacionados:**
- [[Introdução ao Docker e Conteinerização]]
- [[O que são Containers (Detalhes Técnicos)]]
- [[Docker]]
