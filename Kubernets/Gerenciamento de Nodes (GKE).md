# Gerenciamento de Nodes no GKE

No Google [[Kubernetes]] Engine, os nodes (nós) são máquinas virtuais (Compute Engine) agrupadas em **Node Pools** (Grupos de Nós). Um Node Pool é um subconjunto de máquinas dentro de um cluster que possuem a mesma configuração.

## 1. Criando um Novo Node Pool
Se você já tem um cluster e deseja adicionar mais máquinas (ou máquinas com configurações diferentes, como mais RAM ou GPU):

```bash
gcloud container node-pools create pool-adicional \
    --cluster meu-cluster \
    --region us-central1 \
    --num-nodes 2 \
    --machine-type e2-medium
```

## 2. Escalando Nodes Existentes
Você pode aumentar ou diminuir o número de máquinas em um pool existente manualmente:

```bash
gcloud container clusters resize meu-cluster \
    --node-pool default-pool \
    --num-nodes 5 \
    --region us-central1
```

## 3. Ativando o Autoscaling (Escalonamento Automático)
A melhor prática no GKE é deixar o Google gerenciar a quantidade de nós com base na carga de trabalho (CPU/Memória solicitada pelos Pods):

```bash
gcloud container clusters update meu-cluster \
    --enable-autoscaling \
    --node-pool default-pool \
    --min-nodes 1 \
    --max-nodes 10 \
    --region us-central1
```

## 4. Verificando a Conexão dos Nodes
Após subir ou alterar os nodes, verifique se eles estão "Ready" (Prontos) e conectados ao Control Plane do Kubernetes:

```bash
# Lista todos os nodes do cluster
kubectl get nodes

# Mostra detalhes técnicos e labels dos nodes
kubectl get nodes -o wide
```

## 5. Atualizando a Versão dos Nodes
Para manter a segurança e performance, você deve atualizar a versão do Kubernetes nos nodes para coincidir com a do Master:

```bash
gcloud container clusters upgrade meu-cluster \
    --node-pool default-pool \
    --region us-central1
```

---

### Observações Importantes:
- **Preemptible/Spot VMs:** Você pode criar Node Pools com instâncias Spot para economizar até 80% nos custos, ideal para ambientes de teste.
- **Auto-reparo:** O GKE possui um recurso de *Auto-repair* que detecta se um node está saudável e o recria automaticamente caso ele falhe.
