# RBAC e Governança no [[Kubernetes]]

No Kubernetes, a segurança não é apenas sobre perímetros, mas sobre o que cada usuário ou processo pode fazer dentro do cluster. O **RBAC (Role-Based Access Control)** é o mecanismo que regula isso.

## 1. Os Quatro Pilares do RBAC

O RBAC é composto por quatro objetos principais, divididos entre escopo de **Namespace** e escopo de **Cluster**.

### A. Role e ClusterRole (O QUE pode ser feito)
Define um conjunto de permissões (verbos como `get`, `list`, `create`, `delete`) sobre determinados recursos (como `pods`, `services`, `secrets`).
*   **Role:** Permissões restritas a um único Namespace.
*   **ClusterRole:** Permissões que valem para o cluster inteiro (ex: listar Nodes ou Namespaces).

### B. RoleBinding e ClusterRoleBinding (QUEM pode fazer)
Faz a ponte entre a permissão (Role) e o sujeito (Usuário, Grupo ou ServiceAccount).
*   **RoleBinding:** Concede as permissões de uma Role dentro de um Namespace.
*   **ClusterRoleBinding:** Concede permissões em nível de cluster.

## 2. ServiceAccounts (Identidade para Aplicações)

Diferente de usuários humanos, as **ServiceAccounts** são identidades para processos que rodam dentro de Pods.
*   **Cenário comum:** Um Pod de monitoramento (como Prometheus) precisa de uma ServiceAccount com um `ClusterRole` para "ler" as métricas de todos os outros Pods do cluster.
*   **Boa prática:** Nunca use a conta `default`. Crie uma ServiceAccount específica para cada aplicação com o mínimo de permissões necessárias.

## 3. Governança e Limitação de Recursos

Governança no K8s também envolve garantir que um time não "atropele" o outro consumindo todos os recursos.

### ResourceQuotas
Define limites rígidos de consumo para um **Namespace** inteiro.
*   Exemplo: "O time de Desenvolvimento só pode consumir no máximo 10 CPUs e 20GB de RAM no total".

### LimitRanges
Define padrões e limites para **cada container** individual dentro de um Namespace.
*   Impede que alguém crie um Pod sem definir `requests` ou `limits`, garantindo que todo container tenha um tamanho previsível.

## 4. Melhores Práticas de Segurança (Hardening)

1.  **Princípio do Privilégio Mínimo:** Comece com zero permissões e adicione apenas o que for essencial.
2.  **Evite `cluster-admin`:** Evite dar permissões de administrador de cluster para usuários comuns ou aplicações.
3.  **Audite as permissões:** Use ferramentas como `kubectl auth can-i` para testar o que um usuário pode fazer.
    *   `kubectl auth can-i create pods --as=dev-user`
4.  **Namespaces como Fronteiras:** Use Namespaces para isolar times e aplique `NetworkPolicies` junto com RBAC para um isolamento completo.

---
**Links Relacionados:**
- [[Kubernetes]]
- [[Segurança no Docker]]
- [[Troubleshooting no Kubernetes]]
