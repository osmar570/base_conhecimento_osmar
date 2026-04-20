# Como Iniciar no Google [[Kubernetes]] Engine (GKE)

O GKE é a solução gerenciada de Kubernetes do Google Cloud Platform (GCP). Ele elimina a complexidade de gerenciar o *control plane* (plano de controle) do Kubernetes.

## Pré-requisitos

1.  **Conta no GCP:** Ter uma conta ativa no [Google Cloud Console](https://console.cloud.google.com/).
2.  **Projeto Criado:** Um projeto selecionado no console.
3.  **Faturamento Ativo:** Garanta que o Billing esteja ativado para o projeto.
4.  **Google Cloud CLI:** Instalado e configurado localmente (`gcloud components install gke-gcloud-auth-plugin`).

## Passo a Passo para Configuração

### 1. Habilitar a API do Kubernetes
No terminal ou Cloud Shell, execute:
```bash
gcloud services enable container.googleapis.com
```

### 2. Criar um Cluster GKE (Standard)
Comando básico para criar um cluster com 3 nós:
```bash
gcloud container clusters create meu-cluster \
    --region us-central1 \
    --num-nodes 3
```

### 3. Configurar o acesso via Kubectl
Após a criação, obtenha as credenciais para que o `kubectl` possa se comunicar com o cluster:
```bash
gcloud container clusters get-credentials meu-cluster --region us-central1
```

### 4. Verificar a Conexão
Teste se você consegue ver os nós do cluster:
```bash
kubectl get nodes
```

## Dicas de Gerenciamento

-   **Autopilot vs Standard:** O GKE Autopilot é o modo totalmente gerenciado onde o Google cuida de toda a infraestrutura de nós e segurança, enquanto o Standard oferece controle total sobre a configuração dos nós.
-   **Dashboard:** Você pode visualizar e gerenciar seus workloads diretamente pelo Console do Google Cloud na seção "Kubernetes Engine".

## Limpeza (Evitar Custos)
Se não estiver mais usando o cluster, delete-o:
```bash
gcloud container clusters delete meu-cluster --region us-central1
```
