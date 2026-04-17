# Persistência de Dados (Volumes e Bind Mounts)

Por padrão, containers são **efêmeros**: qualquer arquivo criado ou alterado dentro dele é perdido quando o container é removido. Para salvar dados (como bancos de dados) ou compartilhar código, usamos mecanismos de persistência.

## 1. Tipos de Persistência

Existem duas formas principais de persistir dados no Docker:

### A. Volumes (Gerenciados pelo Docker)
São armazenados em uma parte do sistema de arquivos do host que é **gerenciada pelo Docker** (`/var/lib/docker/volumes/` no Linux).
*   **Quando usar:** Produção, bancos de dados, compartilhamento de dados entre múltiplos containers.
*   **Vantagens:** Mais performáticos em Docker Desktop (Mac/Windows), fáceis de fazer backup, não dependem da estrutura de pastas do seu computador.

### B. Bind Mounts (Caminho do Host)
Mapeiam um arquivo ou diretório **específico** do seu computador para dentro do container.
*   **Quando usar:** Desenvolvimento (Hot Reload), arquivos de configuração específicos.
*   **Vantagens:** Você pode editar o código no seu VS Code e o container vê a mudança instantaneamente.

---

## 2. Desenvolvimento em Tempo Real (Hot Reload)

Para que sua aplicação atualize automaticamente enquanto você coda (sem precisar reconstruir a imagem), você deve usar um **Bind Mount**.

### Exemplo com Docker Run:
```bash
docker run -d \
  -p 3000:3000 \
  -v $(pwd):/app \
  minha-app-node
```

### Exemplo com Docker Compose (Recomendado):
```yaml
services:
  web:
    build: .
    volumes:
      - .:/app # Mapeia a pasta atual para /app no container
      - /app/node_modules # "Anonymus Volume" para não sobrescrever os pacotes do container com os locais
```
*Dica: Ao usar frameworks como React, Node ou Python, o Bind Mount garante que o "Watch Mode" do framework detecte a mudança no arquivo.*

---

## 3. Ciclo de Vida dos Volumes Gerenciados

Diferente dos containers, os **Volumes** possuem um ciclo de vida independente:

1.  **Criação:** Ocorre quando você roda um container com um novo volume ou usa `docker volume create`.
2.  **Persistência:** Se você deletar o container (`docker rm -f`), o volume **continua existindo** com todos os dados intactos.
3.  **Reutilização:** Ao subir um novo container (mesmo que seja uma versão mais nova da imagem) e apontar para o mesmo volume, os dados estarão lá.
4.  **Remoção Manual:** Volumes só são deletados se você solicitar explicitamente.

### Comandos de Gerenciamento:
*   `docker volume ls`: Lista volumes órfãos ou em uso.
*   `docker volume inspect <nome>`: Mostra onde os dados estão fisicamente no host.
*   `docker volume rm <nome>`: Deleta o volume (ação irreversível).
*   `docker volume prune`: **Cuidado!** Deleta todos os volumes que não estão sendo usados por nenhum container.

## 4. Resumo: Qual escolher?

| Recurso | Volumes | Bind Mounts |
| :--- | :--- | :--- |
| **Localização no Host** | Gerenciada pelo Docker | Definida pelo usuário |
| **Performance** | Alta (Nativo) | Pode ser lenta em Mac/Windows |
| **Uso em Produção** | Recomendado ✅ | Evitar ❌ |
| **Hot Reload (Dev)** | Não recomendado ❌ | Recomendado ✅ |

---
**Links Relacionados:**
- [[Docker Compose]]
- [[O que são Containers (Detalhes Técnicos)]]
