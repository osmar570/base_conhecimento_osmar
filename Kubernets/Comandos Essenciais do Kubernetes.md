# Comandos Essenciais do [[Kubernetes]] (kubectl)

Guia de referência rápida para os comandos mais utilizados no dia a dia com Kubernetes.

## 1. Informações do Cluster e Contexto
```bash
# Verificar a versão do client e do server
kubectl version

# Exibir informações sobre o cluster
kubectl cluster-info

# Listar contextos (clusters, usuários e namespaces configurados)
kubectl config get-contexts

# Mudar para um contexto específico
kubectl config use-context <nome-do-contexto>

# Definir um namespace padrão para o contexto atual
kubectl config set-context --current --namespace=<nome-do-namespace>
```

## 2. Gerenciamento de Pods
```bash
# Listar todos os pods no namespace atual
kubectl get pods

# Listar pods em todos os namespaces
kubectl get pods -A

# Obter detalhes de um pod específico (incluindo eventos)
kubectl describe pod <nome-do-pod>

# Ver logs de um pod
kubectl logs <nome-do-pod>

# Ver logs em tempo real (tail)
kubectl logs -f <nome-do-pod>

# Executar um comando interativo dentro de um container
kubectl exec -it <nome-do-pod> -- /bin/bash

# Criar um pod temporário para testes de rede
kubectl run busybox --image=busybox -it --rm -- restart=Never -- sh
```

## 3. Gerenciamento de Deployments e Services
```bash
# Listar Deployments
kubectl get deployments

# Escalar um deployment (ex: para 3 réplicas)
kubectl scale deployment <nome-do-deployment> --replicas=3

# Reiniciar um deployment (rollout)
kubectl rollout restart deployment <nome-do-deployment>

# Verificar o status de um rollout
kubectl rollout status deployment <nome-do-deployment>

# Listar Services
kubectl get services (ou svc)

# Expor um deployment como um Service (ClusterIP, NodePort ou LoadBalancer)
kubectl expose deployment <nome> --port=80 --target-port=8080 --type=NodePort
```

## 4. Manipulação de Manifestos (YAML)
```bash
# Aplicar ou atualizar recursos a partir de um arquivo
kubectl apply -f arquivo.yaml

# Deletar recursos definidos em um arquivo
kubectl delete -f arquivo.yaml

# Gerar o YAML de um recurso existente (sem alterar nada)
kubectl get pod <nome-do-pod> -o yaml

# Testar a criação de um recurso e gerar o YAML (Dry Run)
kubectl create deployment nginx --image=nginx --dry-run=client -o yaml > deployment.yaml
```

## 5. Troubleshooting e Monitoramento
```bash
# Listar eventos do cluster (ordenados por tempo)
kubectl get events --sort-by='.lastTimestamp'

# Ver consumo de CPU e Memória dos Nodes
kubectl top nodes

# Ver consumo de CPU e Memória dos Pods
kubectl top pods

# Port-forward para acessar um pod localmente
kubectl port-forward <nome-do-pod> 8080:80
```

## 6. Nodes e Manutenção
```bash
# Listar nodes
kubectl get nodes

# Marcar um node como não agendável (Cordon)
kubectl cordon <nome-do-node>

# Esvaziar um node para manutenção (Drenar)
kubectl drain <nome-do-node> --ignore-daemonsets

# Tornar o node agendável novamente (Uncordon)
kubectl uncordon <nome-do-node>
```
