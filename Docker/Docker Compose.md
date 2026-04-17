# Docker Compose

O **Docker Compose** é uma ferramenta que permite definir e rodar aplicações multi-container de forma orquestrada. Enquanto o Docker CLI foca em gerenciar um container por vez, o Compose gerencia uma "stack" (pilha) inteira de serviços através de um único arquivo de configuração.

## 1. O que é o arquivo `docker-compose.yml`?

É um arquivo em formato YAML que funciona como o "projeto" da sua infraestrutura. Nele, você descreve todos os componentes da sua aplicação (banco de dados, backend, frontend, rede, volumes) para que possam ser iniciados juntos.

A estrutura básica segue este padrão:

```yaml
version: '3.8' # Versão do formato do Compose

services:
  app: # Nome do serviço
    build: . # Constrói a imagem a partir de um Dockerfile local
    ports:
      - "3000:3000"
    depends_on:
      - db # Garante que o banco suba antes da aplicação

  db:
    image: postgres:15 # Usa uma imagem pronta do Docker Hub
    environment:
      POSTGRES_PASSWORD: exemplo
```

## 2. Definindo Componentes no Arquivo

### Serviços (Services)
Representam os containers que compõem sua aplicação. Cada serviço define como ele deve ser construído ou qual imagem deve baixar, além de variáveis de ambiente e políticas de reinicialização.

### Redes (Networks)
Por padrão, o Compose cria uma rede única para sua aplicação, permitindo que os serviços se comuniquem usando apenas o **nome do serviço** como hostname (ex: a `app` consegue acessar o banco apenas chamando `db:5432`).
*   Você pode definir redes personalizadas para isolar grupos de containers.

### Volumes
Essenciais para a [[O que são Containers (Detalhes Técnicos)#4. Efemeridade e Persistência|Persistência de Dados]].
*   **Named Volumes:** Gerenciados pelo Docker (ex: `db_data:/var/lib/postgresql/data`).
*   **Bind Mounts:** Mapeiam pastas do seu computador para o container (ideal para desenvolvimento).

## 3. Comandos Essenciais

O CLI do Compose simplifica o gerenciamento do ciclo de vida:

| Comando | Descrição |
| :--- | :--- |
| `docker-compose up` | Cria e inicia todos os containers definidos. |
| `docker-compose up -d` | Inicia em modo "detached" (em segundo plano). |
| `docker-compose down` | Para e remove os containers, redes e imagens da stack. |
| `docker-compose ps` | Lista o status dos containers gerenciados por aquele arquivo. |
| `docker-compose logs -f` | Exibe e acompanha os logs de todos os serviços simultaneamente. |

## 4. Por que usar Docker Compose?

1.  **Padronização:** Todo desenvolvedor do time sobe o mesmo ambiente com um comando.
2.  **Agilidade:** Não é necessário digitar comandos longos do `docker run` com dezenas de flags.
3.  **Isolamento:** Permite rodar múltiplas stacks isoladas no mesmo host sem conflitos de rede.

---
**Links Relacionados:**
- [[Docker]]
- [[O que são Containers (Detalhes Técnicos)]]
- [[O que é uma Imagem Docker]]
