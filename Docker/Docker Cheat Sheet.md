# Docker Cheat Sheet (Comandos Essenciais)

Este guia reúne os comandos mais utilizados no Docker, organizados por categoria para facilitar a consulta rápida.

## 1. Gerenciamento de Containers

| Comando | Descrição |
| :--- | :--- |
| `docker run <imagem>` | Cria e inicia um container a partir de uma imagem. |
| `docker run -d <imagem>` | Inicia o container em segundo plano (detached mode). |
| `docker ps` | Lista os containers que estão em execução no momento. |
| `docker ps -a` | Lista todos os containers (executando ou parados). |
| `docker stop <id/nome>` | Para a execução de um container. |
| `docker start <id/nome>` | Inicia um container que estava parado. |
| `docker rm <id/nome>` | Remove um container parado. |
| `docker rm -f <id/nome>` | Força a remoção de um container (mesmo em execução). |
| `docker exec -it <id/nome> bash` | Entra no terminal de um container em execução. |
| `docker logs -f <id/nome>` | Visualiza os logs do container em tempo real. |

## 2. Gerenciamento de Imagens

| Comando | Descrição |
| :--- | :--- |
| `docker images` | Lista todas as imagens baixadas localmente. |
| `docker build -t <nome> .` | Constrói uma imagem a partir de um Dockerfile no diretório atual. |
| `docker pull <imagem>` | Baixa uma imagem do Docker Hub sem executá-la. |
| `docker rmi <id/nome>` | Remove uma imagem local. |
| `docker tag <id> <usuario>/<repo>:<tag>` | Adiciona uma tag/nome a uma imagem para envio ao Registry. |
| `docker push <usuario>/<repo>:<tag>` | Envia uma imagem para o Docker Hub ou Registry privado. |

## 3. Redes e Volumes

| Comando | Descrição |
| :--- | :--- |
| `docker network ls` | Lista todas as redes criadas. |
| `docker network create <nome>` | Cria uma nova rede isolada. |
| `docker volume ls` | Lista todos os volumes gerenciados pelo Docker. |
| `docker volume create <nome>` | Cria um novo volume persistente. |
| `docker volume prune` | Remove todos os volumes não utilizados (cuidado!). |

## 4. Docker Compose (Multiserviços)

| Comando | Descrição |
| :--- | :--- |
| `docker-compose up` | Sobe todos os serviços definidos no `docker-compose.yml`. |
| `docker-compose up -d` | Sobe a stack inteira em segundo plano. |
| `docker-compose down` | Para e remove containers, redes e volumes da stack. |
| `docker-compose logs -f` | Acompanha os logs de todos os serviços da stack. |
| `docker-compose ps` | Lista o status dos serviços da stack atual. |

## 5. Limpeza e Manutenção

| Comando | Descrição |
| :--- | :--- |
| `docker system df` | Exibe o uso de disco por containers, imagens e volumes. |
| `docker system prune` | Remove containers parados, redes não usadas e imagens orfãs. |
| `docker stats` | Monitora em tempo real o uso de CPU e Memória dos containers. |

---
**Links Relacionados:**
- [[Introdução ao Docker e Conteinerização]]
- [[Docker Compose]]
- [[Troubleshooting no Docker]]
