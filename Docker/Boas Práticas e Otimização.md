# Boas Práticas e Otimização em Docker

Otimizar suas imagens e o processo de build não serve apenas para economizar disco; isso acelera o CI/CD, reduz custos de transferência (egress) e, principalmente, **aumenta a segurança** ao reduzir a superfície de ataque.

## 1. Escolha de Imagens Base Leves

A escolha da imagem no comando `FROM` é o ponto de partida.

*   **Alpine Linux:** Uma distribuição extremamente leve (~5MB). Imagens como `node:alpine` ou `python:alpine` são muito menores que as versões baseadas em Debian/Ubuntu.
    *   *Ponto de atenção:* Usa `musl libc` em vez de `glibc`, o que pode causar problemas em aplicações C/C++ complexas.
*   **Distroless:** Imagens mantidas pelo Google que contêm apenas a sua aplicação e as dependências de runtime. Elas **não possuem shell** (não dá para dar `docker exec -it bin/sh`), o que as torna incrivelmente seguras e leves.

## 2. Multi-stage Builds

Esta é a técnica mais poderosa para reduzir o tamanho da imagem. Ela permite que você use imagens pesadas para compilar o código e mova apenas o binário final para uma imagem leve.

```dockerfile
# Estágio 1: Build
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Estágio 2: Produção (Apenas o necessário)
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
# A imagem final terá apenas o Nginx e os arquivos estáticos, 
# sem o Node.js ou a pasta node_modules de 1GB.
```

## 3. Ordem das Camadas e Cache

O Docker constrói imagens em camadas. Se uma camada não mudou, ele usa o cache. Se uma camada muda, todas as camadas abaixo dela são reconstruídas.

**❌ Prática Ruim (Invalida o cache toda hora):**
```dockerfile
COPY . .
RUN npm install  # Se você mudar um comentário no código, o npm install roda de novo.
```

**✅ Prática Recomendada:**
```dockerfile
COPY package*.json ./
RUN npm install  # O cache só quebra se o package.json mudar.
COPY . .         # O código muda com frequência, então fica por último.
```

## 4. Uso do `.dockerignore`

Assim como o `.gitignore`, este arquivo evita que arquivos desnecessários sejam enviados para o contexto do Docker (Docker Daemon) durante o build.

**O que incluir no `.dockerignore`:**
*   `.git`
*   `node_modules` ou `venv`
*   `dist` ou `build` (pastas locais)
*   Arquivos de log e segredos (`.env`)

Isso torna o comando `COPY . .` mais rápido e evita que arquivos sensíveis ou lixo local parem dentro da imagem.

## 5. Minimize o número de camadas

Cada comando `RUN`, `COPY` ou `ADD` cria uma camada. Para arquivos pequenos, tente agrupar comandos:

```dockerfile
# Em vez de:
RUN apt-get update
RUN apt-get install -y git

# Use:
RUN apt-get update && apt-get install -y \
    git \
    curl \
    && rm -rf /var/lib/apt/lists/*
```
*Note que limpar o cache do gerenciador de pacotes no mesmo comando `RUN` é essencial para realmente economizar espaço.*

---
**Links Relacionados:**
- [[O que é uma Imagem Docker]]
- [[O que são Containers (Detalhes Técnicos)]]
- [[Docker Compose]]
