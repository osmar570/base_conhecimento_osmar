# Guia Prático de GitOps (Argo CD)

Este guia ensina como iniciar, operar e monitorar um fluxo de GitOps usando o **Argo CD**, transformando seu repositório Git no controle remoto do seu cluster Kubernetes.

## 1. Como Iniciar (Instalação)

O Argo CD roda dentro do seu cluster e precisa de permissões administrativas para gerenciar outros recursos.

### Instalação Básica
```bash
# Cria o namespace dedicado
kubectl create namespace argocd

# Aplica o manifesto oficial de instalação
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Acessando o Painel (Dashboard)
Por padrão, o servidor do Argo CD não é exposto externamente. Você pode usar um `port-forward`:
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
*   **Login:** `admin`
*   **Senha:** Recuperada com o comando:
    `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`

---

## 2. Como Trabalhar (O Fluxo GitOps)

Para o GitOps funcionar, você precisa de dois componentes: um **Repitório Git** com seus YAMLs e um objeto **Application** no Argo CD.

### Definindo sua primeira Application
Crie um arquivo chamado `app-minha-infra.yaml`:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: minha-app-exemplo
  namespace: argocd
spec:
  project: default
  source:
    repoURL: 'https://github.com/seu-usuario/seu-repo-config'
    targetRevision: HEAD
    path: k8s-manifests # Pasta dentro do repo onde estão os YAMLs
  destination:
    server: 'https://kubernetes.default.svc'
    namespace: prod
  syncPolicy:
    automated: # Ativa a reconciliação automática
      prune: true # Deleta recursos no K8s que foram removidos do Git
      selfHeal: true # Corrige mudanças manuais feitas via kubectl
```

Aplique este arquivo: `kubectl apply -f app-minha-infra.yaml`.

---

## 3. Como Executar e Monitorar

O monitoramento no GitOps não é apenas ver se o Pod está rodando, mas sim verificar a **Sincronia**.

### Monitoramento via CLI
*   **Listar Apps:** `argocd app list`
*   **Verificar Saúde:** `argocd app get minha-app-exemplo`
*   **Sincronizar Manualmente:** `argocd app sync minha-app-exemplo` (caso o modo automático esteja desligado).

### Estados de Sincronia no Dashboard
Ao observar o painel do Argo CD, você verá dois indicadores cruciais:

1.  **Sync Status:**
    *   `Synced`: O que está no Git é exatamente o que está no cluster.
    *   `OutOfSync`: Alguém alterou o Git, mas o cluster ainda não atualizou.
2.  **Health Status:**
    *   `Healthy`: A aplicação está rodando sem erros.
    *   `Degraded`: Os recursos existem, mas estão falhando (ex: CrashLoopBackOff).

---

## 4. Troubleshooting: Quando o GitOps trava

Se o Argo CD não consegue sincronizar:

1.  **Permission denied:** Verifique se a `ServiceAccount` do Argo CD tem permissões de RBAC no namespace de destino.
2.  **Comparison Error:** O YAML no Git pode estar mal formatado. O Argo CD mostrará o erro de parser no painel.
3.  **Sync Failed:** Se um recurso (como um Service) não pode ser atualizado devido a campos imutáveis, você pode precisar marcar a opção `Replace` na política de sincronia.

---
**Links Relacionados:**
- [[GitOps e CD Moderno]] (Conceitos Teóricos)
- [[RBAC e Governança]] (Essencial para permissões do Argo)
- [[Troubleshooting no Kubernetes]]
