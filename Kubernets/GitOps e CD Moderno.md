# GitOps: A Operação Moderna de Kubernetes

**GitOps** é um modelo operacional onde a "Fonte da Verdade" de todo o sistema é um repositório Git. Em vez de usar comandos manuais como `kubectl apply`, você descreve o estado desejado no Git, e um agente dentro do cluster garante que a realidade corresponda a essa descrição.

## 1. Os Quatro Princípios do GitOps

Para um sistema ser considerado GitOps, ele deve seguir estes pilares (definidos pelo OpenGitOps):

1.  **Declarativo:** Todo o sistema deve ser descrito de forma declarativa (YAMLs, Helm Charts, Kustomize).
2.  **Versionado e Imutável:** O estado desejado é armazenado em um sistema que permite versionamento e histórico (Git).
3.  **Puxado Automaticamente:** Agentes de software detectam mudanças no Git e aplicam no cluster automaticamente.
4.  **Reconciliação Contínua:** O sistema monitora constantemente a "deriva" (drift). Se alguém mudar algo manualmente no cluster, o agente GitOps sobrescreve para voltar ao que está no Git.

## 2. Por que usar GitOps? (Push vs. Pull)

### O Modelo Tradicional (CI/CD Push)
O seu pipeline (Jenkins, GitHub Actions) tem as credenciais do cluster e "empurra" o comando `kubectl apply`.
*   **Problema:** Se o cluster cair ou alguém mudar algo manualmente, o pipeline não sabe. O acesso ao cluster fica espalhado em várias ferramentas de CI.

### O Modelo GitOps (CD Pull)
Um operador (como ArgoCD ou Flux) roda **dentro** do cluster. Ele não recebe ordens; ele observa o Git.
*   **Vantagem:** O cluster se auto-recupera. Se você deletar um Service por erro, o operador GitOps o recria em segundos porque "no Git diz que ele deve existir".

## 3. Ferramentas Principais

*   **ArgoCD:** A ferramenta mais popular. Possui uma interface gráfica poderosa que mostra visualmente a saúde de cada recurso e a sincronia com o Git.
*   **FluxCD:** Focado em ser leve e seguir a filosofia Unix. É altamente modular e excelente para automação pura via código.

## 4. O Fluxo de Trabalho (Workflow)

1.  **Dev** faz um Pull Request (PR) alterando a tag da imagem no YAML da aplicação.
2.  **Equipe** revisa e aprova o PR.
3.  **Merge** para a branch `main`.
4.  **Operador GitOps** detecta o novo commit.
5.  **Sincronização:** O operador aplica as mudanças no Kubernetes.
6.  **Resultado:** A nova versão está no ar sem que ninguém tenha rodado um comando no terminal.

## 5. Benefícios para a Equipe

*   **Auditabilidade:** Quem mudou o quê e quando? Está tudo no log do Git.
*   **Rollback Instantâneo:** Deu erro na produção? Basta dar um `git revert` no commit anterior e o cluster volta ao estado estável automaticamente.
*   **Segurança:** As credenciais de admin do cluster ficam apenas dentro do cluster (com o Argo/Flux), e não expostas em ferramentas de CI externas.
*   **Disaster Recovery:** Se o seu cluster for destruído, basta criar um novo e apontar o operador GitOps para o repositório. O cluster inteiro se reconstrói sozinho.

---
**Links Relacionados:**
- [[Kubernetes]]
- [[Helm - Gerenciador de Pacotes]]
- [[RBAC e Governança]]
