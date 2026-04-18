# Gateway API e HTTPRoute

A **Gateway API** é a evolução moderna do antigo objeto `Ingress`. Ela foi criada para oferecer um roteamento de rede mais expressivo, extensível e orientado a papéis dentro do [[Kubernetes]].

## 1. Por que substituir o Ingress?

O `Ingress` original era limitado e dependia fortemente de "Annotations" (anotações) específicas de cada fabricante (Nginx, Traefik, ALB) para realizar tarefas comuns como redirecionamentos ou testes Canary. Isso tornava o código difícil de portar entre diferentes provedores.

A Gateway API resolve isso criando uma estrutura modular e padronizada.

## 2. A Estrutura Orientada a Papéis

A Gateway API separa a infraestrutura da lógica de negócio através de três objetos principais:

### A. GatewayClass (O Fabricante)
Define o controlador que implementa a API (ex: Istio, Nginx, Cilium, Google Cloud Load Balancer). Geralmente gerenciado pelo **Administrador do Cluster**.

### B. Gateway (A Infraestrutura)
Define onde o tráfego entra (IPs, Portas, Protocolos e Certificados TLS). Gerenciado pelo **Operador de Infraestrutura/Plataforma**.

### C. HTTPRoute (A Regra da App)
Define como o tráfego é roteado para os Services (caminhos, cabeçalhos, pesos para Canary). Gerenciado pelos **Desenvolvedores da Aplicação**.

## 3. Exemplo de Configuração

### Definindo o Gateway (Porta de Entrada)
```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: gateway-producao
  namespace: infra-rede
spec:
  gatewayClassName: nginx-gateway
  listeners:
  - name: http
    protocol: HTTP
    port: 80
    allowedRoutes:
      namespaces:
        from: All # Permite que apps de qualquer namespace usem este gateway
```

### Definindo o HTTPRoute (Roteamento da App)
```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: rota-meu-servico
  namespace: app-backend
spec:
  parentRefs:
  - name: gateway-producao
    namespace: infra-rede
  hostnames:
  - "api.minhaempresa.com"
  rules:
  - matches:
    - path:
        type: PathPrefix
        value: /v1
    backendRefs:
    - name: servico-v1
      port: 8080
```

## 4. Vantagens do HTTPRoute sobre o Ingress

1.  **Canary Deployment Nativo:** Você pode dividir o tráfego entre duas versões de uma aplicação usando o campo `weight` (peso) diretamente no YAML, sem anotações extras.
2.  **Modificação de Cabeçalhos:** Permite adicionar ou remover headers de requisição/resposta de forma padronizada.
3.  **Compartilhamento de Gateway:** Múltiplas equipes podem "conectar" suas `HTTPRoutes` em um único `Gateway` centralizado de forma segura.

---
**Links Relacionados:**
- [[Kubernetes]]
- [[Estratégias de Deployment]] (Canary)
- [[Terraform/Exemplo Completo - K8s, Rancher e Gateway API]]
