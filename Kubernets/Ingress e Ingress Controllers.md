# Ingress e Ingress Controllers

Enquanto um [[Objetos Fundamentais|Service]] do tipo LoadBalancer cria um balanceador de carga para cada serviço exposto (o que pode ser caro e difícil de gerenciar), o **Ingress** atua como uma "porta de entrada inteligente" para o cluster.

## 1. O que é o Ingress?
O Ingress é um objeto que gerencia o acesso externo aos serviços no cluster, tipicamente via HTTP e HTTPS. Ele permite consolidar várias regras de roteamento em um único recurso.

**Principais funções:**
- Roteamento baseado em caminhos (ex: `meusite.com/api` -> serviço-api).
- Roteamento baseado em domínios (ex: `app1.site.com` -> serviço1).
- Terminação de TLS/SSL (gerenciamento de certificados HTTPS).

## 2. O que é o Ingress Controller?
Diferente de outros [[Objetos Fundamentais]] que rodam nativamente no plano de controle, o Ingress **precisa de um Controller instalado** para funcionar. O Ingress é apenas a "regra", o Controller é o "motor" (servidor proxy) que executa essas regras.

Exemplos populares:
- NGINX Ingress Controller.
- Traefik.
- Istio Ingress Gateway.
- GCE Ingress (Nativo do [[como iniciar (GKE)]]).

---

## 3. Como instalar um Ingress Controller

### A. NGINX (Ambientes Locais ou Outros)
Se você estiver em um ambiente [[como iniciar (Local)]] ou Kubernetes Bare-metal, você pode instalar o NGINX Ingress via Helm ou manifesto oficial:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```

### B. GKE (Ingress Nativo do Google)
No [[como iniciar (GKE)]], o controller **GCE Ingress** já vem instalado por padrão. Ele é altamente integrado com a infraestrutura do Google Cloud.

- **Vantagem:** Cria automaticamente um **Google Cloud HTTP(S) Load Balancer**.
- **Configuração:** Não precisa instalar nada, basta usar a anotação correta no seu YAML.

---

## 4. Criando um Recurso de Ingress (YAML)

### Exemplo para NGINX:
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: meu-ingress-nginx
  annotations:
    kubernetes.io/ingress.class: "nginx" # Define que o Nginx deve gerenciar esta regra
spec:
  rules:
  - host: meu-app.exemplo.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nginx-service
            port:
              number: 80
```

### Exemplo para GKE (Nativo):
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: meu-ingress-gke
  annotations:
    kubernetes.io/ingress.class: "gce" # Usa o Load Balancer do Google Cloud
spec:
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nginx-service
            port:
              number: 80
```

---

## 5. Por que usar Ingress?
1.  **Economia:** Você usa apenas um IP público (LoadBalancer) para vários serviços.
2.  **Centralização:** Gerencia SSL/TLS em um único lugar em vez de em cada aplicação.
3.  **Flexibilidade:** Permite criar regras complexas de tráfego, como Canary Deployments ou A/B Testing.

### Relação com outros objetos:
- O **Ingress** envia o tráfego para um **Service**.
- O **Service** distribui o tráfego para os **Pods**.
- O **Ingress Controller** monitora o cluster em busca de novos objetos Ingress para atualizar sua configuração de proxy automaticamente.
