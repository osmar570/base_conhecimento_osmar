# Autoscaling no [[Kubernetes]]

O **Autoscaling** é um dos recursos mais poderosos do Kubernetes. Ele permite que o sistema cresça automaticamente durante picos de tráfego e encolha quando a demanda diminui, otimizando custos e garantindo a disponibilidade.

Existem três tipos principais de escalonamento:

---

## 1. HPA (Horizontal Pod Autoscaler)
O **HPA** ajusta o número de réplicas de um [[Objetos Fundamentais|Pod]] com base no consumo de recursos (geralmente CPU ou Memória).

*   **Como funciona:** Ele observa as métricas dos Pods. Se o uso de CPU ultrapassar o limite definido, o HPA avisa o Deployment para criar mais Pods.
*   **Exemplo de YAML:**
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: minha-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: minha-app # Alvo do escalonamento
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 60 # Mantém a CPU em média em 60%
```

---

## 2. VPA (Vertical Pod Autoscaler)
Em vez de criar mais Pods, o **VPA** aumenta ou diminui o "tamanho" (CPU e Memória) de um Pod existente.

*   **Uso ideal:** Aplicações que não conseguem ser replicadas horizontalmente (ex: alguns tipos de bancos de dados ou processos legados).
*   **Observação:** Geralmente, o VPA requer que o Pod seja reiniciado para aplicar os novos limites de recursos.

---

## 3. Cluster Autoscaler (CA)
Enquanto o HPA e o VPA cuidam dos Pods, o **Cluster Autoscaler** cuida da infraestrutura física (os Nodes).

*   **Como funciona:** Se o HPA tentar criar novos Pods e não houver mais espaço nos servidores existentes, o CA solicita ao provedor de nuvem (como o [[como iniciar (GKE)|GKE]]) para criar um novo servidor.
*   **Economia:** Quando os servidores ficam vazios porque a demanda baixou, o CA remove os Nodes excedentes para economizar dinheiro.

---

## 4. Requisito Fundamental: Metrics Server
Para que o HPA e o VPA funcionem, o cluster precisa ter um componente instalado chamado **Metrics Server**, que coleta os dados de consumo dos containers.

No [[como iniciar (GKE)]], ele já vem habilitado por padrão. No [[como iniciar (Local)]], você pode precisar habilitá-lo:
```bash
minikube addons enable metrics-server
```

---

## Boas Práticas
1.  **Defina Resources Requests:** O Kubernetes só consegue escalar se souber quanto de CPU/RAM sua aplicação usa normalmente. Defina sempre `resources.requests` e `resources.limits` no seu [[Manifestos YAML e Persistência|YAML]].
2.  **Não use HPA e VPA juntos no mesmo recurso:** Isso pode causar conflitos onde um tenta aumentar o número de Pods enquanto o outro tenta aumentar o tamanho deles simultaneamente.
3.  **Teste de Carga:** Sempre faça testes de carga para validar se as regras de escalonamento estão disparando no momento correto.

### Comando Útil:
```bash
# Monitorar o HPA em tempo real
kubectl get hpa -w
```
