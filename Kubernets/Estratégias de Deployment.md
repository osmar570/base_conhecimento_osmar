# Estratégias de Deployment no [[Kubernetes]]

Diferente de sistemas legados onde você precisava de uma "janela de manutenção" para atualizar uma aplicação, o Kubernetes oferece várias estratégias para atualizar versões com o mínimo (ou zero) impacto para o usuário.

## 1. Rolling Update (Padrão)

O Kubernetes substitui gradualmente os Pods da versão antiga pelos da versão nova.
*   **Como funciona:** Ele sobe um novo Pod (v2), espera ele ficar saudável (`Ready`) e então deleta um Pod antigo (v1). Repete o processo até que todos sejam v2.
*   **Vantagem:** Zero downtime e baixo consumo de recursos extras.
*   **Desvantagem:** Durante a transição, duas versões diferentes da aplicação estarão rodando simultaneamente (problemas com banco de dados podem ocorrer).

## 2. Recreate

Deleta todos os Pods da versão antiga antes de subir qualquer Pod da versão nova.
*   **Como funciona:** v1 -> Down -> v2 -> Up.
*   **Vantagem:** Garante que nunca haverá duas versões rodando ao mesmo tempo (útil para migrações de banco de dados complexas).
*   **Desvantagem:** Existe um período de **Downtime** (indisponibilidade) enquanto a nova versão sobe.

## 3. Blue/Green Deployment

Mantém dois ambientes idênticos rodando simultaneamente.
*   **Blue (v1):** A versão atual em produção.
*   **Green (v2):** A nova versão, rodando mas sem receber tráfego público.
*   **Como funciona:** Quando você valida que a versão Green está perfeita, você altera o **Service** ou o **Ingress** para apontar do Blue para o Green.
*   **Vantagem:** Rollback instantâneo (basta apontar de volta para o Blue) e zero downtime.
*   **Desvantagem:** Dobra o custo de infraestrutura durante o deploy.

## 4. Canary Deployment

Libera a nova versão para uma pequena porcentagem de usuários antes de liberar para todos.
*   **Como funciona:** 95% do tráfego vai para a v1 e 5% para a v2 (o "Canário"). Se não houver erros nos logs e métricas, você aumenta gradualmente para 10%, 50% e 100%.
*   **Vantagem:** Permite testar o comportamento da aplicação com tráfego real com risco mínimo.
*   **Desvantagem:** Exige ferramentas avançadas para gerenciar o tráfego (como **Istio**, **Linkerd** ou Nginx Ingress).

## 5. Resumo de Escolha

| Estratégia | Zero Downtime? | Custo de Infra | Risco |
| :--- | :--- | :--- | :--- |
| **Rolling Update** | Sim | Baixo | Médio |
| **Recreate** | Não | Baixo | Médio |
| **Blue/Green** | Sim | Alto | Baixo |
| **Canary** | Sim | Médio | Mínimo |

## 6. Configuração no YAML

Exemplo de um `RollingUpdate` customizado para ser mais rápido:
```yaml
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 25%       # Quantos pods extras podem ser criados acima do desejado
      maxUnavailable: 0   # Garante que nenhum pod antigo seja deletado antes do novo estar pronto
```

---
**Links Relacionados:**
- [[Kubernetes]]
- [[Service Mesh - Istio]] (Essencial para Canary)
- [[GitOps e CD Moderno]]
