# Monitoramento de Nodes e Pods

O monitoramento é essencial para garantir a saúde do cluster, prever falhas e otimizar custos. No [[Kubernetes]], monitoramos basicamente dois níveis: a **Infraestrutura (Nodes)** e as **Aplicações (Pods)**.

---

## 1. Monitoramento Básico (Metrics Server)
O **Metrics Server** é a fonte de dados mínima necessária para que comandos de status e o [[Autoscaling no Kubernetes|HPA]] funcionem. Ele coleta métricas de uso de CPU e Memória.

### Comandos Rápidos:
```bash
# Ver consumo de CPU e Memória de cada Node
kubectl top nodes

# Ver consumo de cada Pod no namespace atual
kubectl top pods

# Ver consumo de containers específicos dentro de um Pod
kubectl top pod nome-do-pod --containers
```

---

## 2. Padrão de Mercado: Prometheus e Grafana
Para um monitoramento histórico e visual, a combinação Prometheus + Grafana é o padrão absoluto.

*   **Prometheus:** Um banco de dados de séries temporais que "puxa" (pull) as métricas dos Nodes e Pods.
*   **Grafana:** A interface visual que transforma esses dados em painéis (dashboards) bonitos e alertas (e-mail, Slack).
*   **Node Exporter:** Um agente que roda em cada Node para coletar métricas de hardware (disco, rede, temperatura).

**Como instalar rapidamente:** Geralmente via [[Helm - Gerenciador de Pacotes]]:
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/kube-prometheus-stack
```

---

## 3. Monitoramento Nativo na Nuvem
Se você usa serviços gerenciados, os provedores oferecem ferramentas integradas que não exigem instalação manual:

*   **GKE:** Integrado ao **Google Cloud Monitoring (Stackdriver)**. Ele já mostra gráficos de saúde do cluster diretamente no console.
*   **AKS:** Integrado ao **Azure Monitor / Container Insights**.
*   **OKE:** Integrado ao **OCI Monitoring**.

---

## 4. O que monitorar? (Métricas Críticas)

### Nos Nodes:
1.  **CPU/Memória Pressure:** Indica se o servidor está ficando sem recursos para novos Pods.
2.  **Disk Pressure:** Indica que o disco está cheio (pode causar a expulsão de Pods).
3.  **Network Throughput:** Picos anômalos de tráfego.

### Nos Pods:
1.  **Restart Count:** Se um Pod está reiniciando muito, há um erro na aplicação (CrashLoopBackOff).
2.  **OOMKill (Out of Memory):** Indica que o container tentou usar mais memória do que o limite definido no [[Manifestos YAML e Persistência|YAML]].
3.  **Liveness/Readiness Probes:** Verificam se a aplicação está viva e pronta para receber tráfego.

---

## 5. Logs (Onde estão os erros?)
Monitorar números é importante, mas os logs dizem *por que* algo falhou.

*   **Ver logs de um Pod:** `kubectl logs nome-do-pod`
*   **Seguir logs em tempo real:** `kubectl logs -f nome-do-pod`
*   **Logs de containers que crasharam:** `kubectl logs nome-do-pod --previous`

Para centralização de logs em larga escala, usa-se a pilha **Loki** (da Grafana) ou **ELK/EFK** (Elasticsearch, Fluentd, Kibana).

---
*Links relacionados:*
- [[Autoscaling no Kubernetes]]
- [[Objetos Fundamentais]]
- [[como iniciar (GKE)]]
