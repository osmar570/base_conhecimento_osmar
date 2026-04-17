# Redes no Docker

O Docker possui um subsistema de rede flexível que permite que os containers se comuniquem entre si e com o mundo exterior.

## 1. Drivers de Rede (Tipos de Rede)

O Docker usa "drivers" para definir como a rede se comporta:

*   **Bridge (Padrão):** É o driver padrão. Cria uma rede virtual interna no host. Containers na mesma rede bridge podem falar entre si usando IPs ou nomes de serviço (no Compose).
*   **Host:** Remove o isolamento de rede entre o container e o host. O container usa o IP e as portas do seu computador diretamente. (Melhor performance, menos isolamento).
*   **None:** Desativa toda a rede do container. Útil para jobs de processamento que não precisam de acesso externo.
*   **Overlay:** Usado para comunicação entre múltiplos hosts (Docker Swarm ou clusters). Permite que um container no Host A fale com um container no Host B como se estivessem na mesma rede.

## 2. Comunicação e DNS Interno

O Docker possui um servidor DNS embutido. Quando você cria uma rede personalizada (User-defined bridge):
*   Você não precisa saber o IP do container.
*   Pode usar o **nome do container** ou o **alias do serviço** como endereço.
*   Exemplo: Uma aplicação Flask pode se conectar ao banco usando `db:5432` em vez de `172.17.0.3`.

## 3. Exposição de Portas (`-p` ou `ports`)

Existe uma diferença crucial entre **Expor** e **Publicar**:
*   **Expose:** Apenas documenta que o container ouve naquela porta (uso interno entre containers).
*   **Publish (`-p`):** Mapeia uma porta do seu Host para a porta do Container.
    *   `docker run -p 8080:80 nginx` -> Acessa o Nginx do container (porta 80) através do seu navegador em `localhost:8080`.

## 4. Comandos Úteis
*   `docker network ls`: Lista todas as redes.
*   `docker network create minha-rede`: Cria uma rede nova.
*   `docker network inspect bridge`: Veja quais containers estão conectados e seus IPs.

---
**Links Relacionados:**
- [[Docker Compose]] (onde redes são definidas no YAML)
- [[O que são Containers (Detalhes Técnicos)]]
