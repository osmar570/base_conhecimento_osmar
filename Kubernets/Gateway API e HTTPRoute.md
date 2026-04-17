# Gateway API e HTTPRoute: A Evolução do Ingress

Com o amadurecimento do [[Kubernetes]], o objeto Ingress tornou-se limitado para cenários complexos. A **Gateway API** surgiu como o sucessor oficial, introduzindo o recurso **HTTPRoute** para gerenciar o tráfego de forma mais eficiente e flexível.

---

## 1. O que é a Gateway API?
Diferente do Ingress, que era um único objeto "faz-tudo", a Gateway API divide as responsabilidades em três partes:

1.  **GatewayClass:** Define o "tipo" de balanceador (configurado pelo admin do cluster).
2.  **Gateway:** O ponto de entrada real (o IP e a porta) que escuta o tráfego.
3.  **HTTPRoute:** Define as regras de roteamento (para onde o tráfego vai). É aqui que o desenvolvedor trabalha.

---

## 2. Por que mudar para HTTPRoute?
- **Padronização:** Resolve o problema de cada Ingress Controller ter suas próprias anotações proprietárias.
- **Roteamento Avançado:** Suporta nativamente divisão de tráfego por peso (Canary), redirecionamentos e modificação de headers sem hacks.
- **Multi-tenancy:** Permite que diferentes equipes gerenciem suas rotas de forma isolada, mas compartilhando o mesmo Gateway.

---

## 3. Como Iniciar (Configuração)

### Passo 1: Instalar as CRDs (Custom Resource Definitions)
A Gateway API não vem instalada por padrão em clusters antigos. Você precisa aplicar as definições oficiais:

```bash
kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.0.0/standard-install.yaml
```
*(Nota: No [[como iniciar (GKE)]], você pode habilitar isso nativamente nas configurações do cluster).*

### Passo 2: Criar o Gateway
Este objeto cria o balanceador de carga físico.

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: meu-gateway
spec:
  gatewayClassName: gke-l7-global-external-managed # Ou nginx-gateway dependendo do provedor
  listeners:
  - name: http
    protocol: HTTP
    port: 80
    allowedRoutes:
      namespaces:
        from: All
```

---

## 4. Configurando o HTTPRoute (O "Router")
Agora, definimos como o tráfego que chega no Gateway deve ser direcionado para os seus [[Objetos Fundamentais|Services]].

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: minha-rota-nginx
spec:
  parentRefs:
  - name: meu-gateway # Conecta esta rota ao Gateway criado acima
  hostnames:
  - "meuapp.com"
  rules:
  - matches:
    - path:
        type: PathPrefix
        value: /api
    backendRefs:
    - name: servico-backend
      port: 8080
  - matches:
    - path:
        type: PathPrefix
        value: /
    backendRefs:
    - name: nginx-service # Do arquivo [[Manifestos YAML e Persistência]]
      port: 80
```

---

## 5. Resumo de Comandos
```bash
# Verificar se as classes de Gateway estão disponíveis
kubectl get gatewayclasses

# Ver o status do seu Gateway (se ele já recebeu um IP)
kubectl get gateways

# Ver as rotas configuradas
kubectl get httproutes
```

A Gateway API é o futuro da rede no Kubernetes. Embora o Ingress ainda funcione, aprender a trabalhar com **HTTPRoute** é essencial para manter seu ambiente atualizado e compatível com as novas ferramentas do ecossistema.
