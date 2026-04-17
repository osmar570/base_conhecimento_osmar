# Orquestração com Kubernetes (K8s)

Quando passamos de rodar apenas alguns [[O que são Containers (Detalhes Técnicos)|Contêineres]] em uma máquina local para gerenciar centenas ou milhares de contêineres em produção, o gerenciamento manual se torna impossível. É aqui que entra a **Orquestração**.

## O que é Orquestração?

Orquestração de contêineres é o processo de automatizar a implantação, o gerenciamento, a escala e a rede de contêineres. Se o Docker fornece o "contêiner", a orquestração fornece o "navio cargueiro" que sabe onde colocar cada um, como empilhá-los e o que fazer se um cair no mar.

## Kubernetes: O Padrão de Mercado

O Kubernetes (também conhecido como **K8s**) é a ferramenta de orquestração mais utilizada no mundo. Criado pelo Google, ele gerencia o ciclo de vida dos contêineres em um cluster de máquinas.

### Docker vs. Kubernetes
Uma confusão comum é achar que eles competem. Na verdade, eles são complementares:
*   **Docker:** Cria e roda contêineres em um único host.
*   **Kubernetes:** Gerencia esses contêineres através de múltiplos hosts (nós), garantindo alta disponibilidade.

## Conceitos Fundamentais do K8s

Para entender o Kubernetes, precisamos conhecer seus objetos principais:

1.  **Nodes (Nós):** São as máquinas (físicas ou virtuais) que formam o cluster.
2.  **Pods:** É a menor unidade do Kubernetes. Um Pod agrupa um ou mais contêineres que compartilham o mesmo armazenamento e rede. No K8s, você não sobe um "contêiner", você sobe um "Pod".
3.  **Deployment:** Define o estado desejado da aplicação (ex: "quero 3 réplicas deste Pod rodando"). Se um Pod morrer, o Deployment cria outro automaticamente.
4.  **Service:** Uma abstração que define como acessar os Pods via rede, funcionando como um balanceador de carga interno.

## Problemas que o Kubernetes resolve

*   **Service Discovery e Load Balancing:** O K8s dá aos contêineres seus próprios endereços IP e um nome DNS único, balanceando o tráfego entre eles.
*   **Self-healing (Auto-recuperação):** Se um contêiner falha, o K8s o reinicia. Se um nó morre, o K8s move os contêineres para outro nó saudável.
*   **Escalabilidade Horizontal:** Você pode aumentar ou diminuir o número de réplicas da aplicação com um único comando ou automaticamente com base no uso de CPU.
*   **Rollouts e Rollbacks Automatizados:** Permite atualizar sua aplicação (nova [[O que é uma Imagem Docker|Imagem Docker]]) sem interrupção (zero-downtime). Se algo der errado, ele volta para a versão anterior sozinho.

## O ecossistema atual
Embora o Docker tenha sido o motor original do Kubernetes, hoje o K8s utiliza o padrão **CRI (Container Runtime Interface)**, o que permite que ele use outros runtimes além do Docker, como o *containerd* ou *CRI-O*, focando na eficiência.

---
**Links Relacionados:**
- [[Introdução ao Docker e Conteinerização]]
- [[O que são Containers (Detalhes Técnicos)]]
- [[O que é uma Imagem Docker]]
