# Objetos Fundamentais do [[Kubernetes]]

Para gerenciar aplicações, o Kubernetes utiliza abstrações chamadas **Objetos**. Os três pilares fundamentais para rodar qualquer aplicação são Pods, Deployments e Services.

---

## 1. Pods
O **Pod** é a menor unidade de execução no Kubernetes. Ele representa um processo único rodando no cluster.

*   **O que é:** Um grupo de um ou mais containers (como Docker) que compartilham o mesmo armazenamento, rede e especificações de como rodar.
*   **Importância:** No Kubernetes, você não sobe containers diretamente; você sobe Pods. Eles garantem que os containers que precisam trabalhar juntos estejam sempre no mesmo host (nó).
*   **Características:** Pods são efêmeros (mortais). Se um Pod falha ou o nó onde ele está morre, o Pod não é "consertado", ele é substituído.

## 2. Deployments
O **Deployment** é o objeto que gerencia a criação e a atualização dos seus Pods.

*   **O que é:** Uma camada de gerenciamento acima dos Pods. Você descreve o "estado desejado" (ex: "quero 3 réplicas do Pod da minha aplicação") e o Deployment se encarrega de manter esse estado.
*   **Importância:**
    *   **Auto-cura (Self-healing):** Se um Pod cair, o Deployment percebe e cria um novo automaticamente.
    *   **Escalabilidade:** Permite aumentar ou diminuir o número de réplicas com um único comando.
    *   **Rollouts e Rollbacks:** Permite atualizar a versão da sua aplicação sem downtime (instala um novo enquanto remove o antigo) e voltar para a versão anterior se algo der errado.

## 3. Services
O **Service** é o objeto que define como acessar os seus Pods.

*   **O que é:** Uma abstração que define uma política de acesso aos Pods (geralmente via rede). Como Pods nascem e morrem com IPs diferentes, o Service fornece um **IP fixo e um nome DNS estável** para eles.
*   **Importância:**
    *   **Service Discovery:** Permite que uma parte da aplicação (ex: Frontend) encontre outra (ex: Backend) sem precisar saber o IP exato de cada Pod.
    *   **Load Balancing (Balanceamento de Carga):** Distribui o tráfego de rede entre todas as réplicas de Pods saudáveis que ele gerencia.
    *   **Exposição:** Define se a aplicação será acessível apenas dentro do cluster (ClusterIP) ou externamente pela Internet (LoadBalancer/NodePort).

---

### Resumo da Hierarquia:
1.  **Service:** O endereço/telefone da aplicação.
2.  **Deployment:** O gerente que garante que os funcionários (Pods) estejam trabalhando.
3.  **Pod:** O funcionário que executa a tarefa (container).
