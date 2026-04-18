# Troubleshooting no Kubernetes

Depurar o Kubernetes exige entender em qual camada o problema está: **Infraestrutura (Node)**, **Orquestração (Control Plane)** ou **Aplicação (Pod)**.

## 1. O Fluxo de Ouro da Depuração

Sempre siga esta ordem para não perder tempo:

1.  **`kubectl get pods`**: Verifique o status geral.
2.  **`kubectl describe pod <nome>`**: O comando mais importante. Ele mostra os **Events**, que dizem por que o Pod falhou ao iniciar.
3.  **`kubectl logs <nome>`**: Se o Pod está `Running` mas não funciona, o erro está no código da aplicação.
4.  **`kubectl get events -A`**: Mostra problemas globais no cluster (falta de recursos, erros de rede).

## 2. Entendendo os Status de Erro

### ImagePullBackOff
O Kubernetes não conseguiu baixar a imagem.
*   **Causas:** Nome da imagem errado, tag inexistente ou falta de autenticação no Registry (falta o `imagePullSecrets`).

### CrashLoopBackOff
O container inicia, mas morre logo em seguida. O K8s tenta reiniciar repetidamente.
*   **Causas:** Erro no código, variável de ambiente faltando, arquivo de configuração não encontrado ou falha na conexão com o banco de dados.
*   **Como fixar:** Olhe os logs (`kubectl logs --previous`).

### Pending
O Pod nem chegou a tentar iniciar.
*   **Causas:** Falta de recursos (CPU/RAM) no cluster ou o `nodeSelector` não encontrou um nó compatível.
*   **Como fixar:** Olhe o `describe` para ver mensagens de "Insufficient cpu".

### OOMKilled (Out Of Memory)
O container tentou usar mais memória do que o limite definido no manifesto YAML.
*   **Como fixar:** Aumente os `resources.limits.memory` ou investigue memory leaks no código.

## 3. Ferramentas de "Cirurgia"

### Acesso Interativo
Se precisar testar a rede de dentro do cluster:
```bash
kubectl exec -it <pod_name> -- /bin/sh
```

### Port-Forward (O Atalho)
Acesse um serviço que não está exposto para a internet diretamente da sua máquina:
```bash
kubectl port-forward pod/<pod_name> 8080:80
```

### Depuração de Redes (Ephemeral Containers)
Se o seu container for "Distroless" (sem shell), use um container efêmero com ferramentas de rede:
```bash
kubectl debug -it <pod_name> --image=nicolaka/netshoot
```

## 4. Problemas no Nó (Node)
Se o comando `kubectl get nodes` mostrar um nó como `NotReady`:
1.  Acesse o servidor via SSH.
2.  Verifique o status do Kubelet: `systemctl status kubelet`.
3.  Verifique o espaço em disco: `df -h` (disco cheio é uma causa comum de falha no nó).

---
**Links Relacionados:**
- [[Kubernetes]]
- [[Comandos Essenciais do Kubernetes]]
- [[Monitoramento de Nodes e Pods]]
