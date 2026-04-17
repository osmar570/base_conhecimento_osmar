# Service Mesh com Istio

Conforme sua arquitetura de microserviços cresce, a comunicação entre eles se torna complexa. O **Istio** é uma **Service Mesh** (Malha de Serviços) que resolve problemas de rede, segurança e observabilidade sem que você precise alterar uma única linha de código da sua aplicação.

---

## 1. O que é uma Service Mesh?
Imagine que você tem dezenas de serviços conversando entre si. Como garantir que a comunicação seja criptografada? Como limitar o tráfego entre eles? Como saber qual serviço está lento?
A Service Mesh adiciona uma camada de infraestrutura que intercepta todo o tráfego de rede do cluster para gerenciar essas questões.

---

## 2. Como o Istio funciona (O Sidecar)
O Istio utiliza o padrão **Sidecar**. Para cada [[Objetos Fundamentais|Pod]] da sua aplicação, o Istio injeta um pequeno container extra chamado **Envoy Proxy**.
- Todo o tráfego que entra ou sai do seu container passa por esse proxy.
- O conjunto desses proxies forma o **Data Plane** (Plano de Dados).
- O componente central do Istio, o **Istiod**, forma o **Control Plane** (Plano de Controle), gerenciando as configurações de todos os proxies.

---

## 3. Principais Recursos

### Gerenciamento de Tráfego
- **Canary Deployments:** Enviar 10% do tráfego para a versão nova e 90% para a antiga.
- **Circuit Breaking:** Interromper chamadas para um serviço que está falhando para evitar um efeito cascata.
- **Retries e Timeouts:** Configurar tentativas automáticas de conexão.

### Segurança
- **mTLS Automático:** Criptografa toda a comunicação entre os Pods por padrão.
- **Políticas de Autorização:** Definir exatamente qual serviço pode conversar com qual (ex: "Só o Frontend pode falar com o Backend").

### Observabilidade
- Gera automaticamente métricas detalhadas e rastreamento (Tracing) de todas as requisições, integrando-se perfeitamente com o [[Monitoramento de Nodes e Pods|Prometheus e Grafana]].

---

## 4. Como Iniciar e Configurar

### Instalação via istioctl
A forma mais comum de instalar é usando o binário oficial `istioctl`:

```bash
istioctl install --set profile=demo -y
```

### Ativando a Injeção Automática
Para que o Istio comece a gerenciar seus Pods, você deve marcar o Namespace:
```bash
kubectl label namespace default istio-injection=enabled
```
*A partir de agora, qualquer novo Pod criado nesse namespace receberá o proxy automaticamente.*

---

## 5. Objetos Principais (Configuração)

### VirtualService
Define as regras de roteamento. É mais potente que o [[Ingress e Ingress Controllers|Ingress]] tradicional.
```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: minha-app-vs
spec:
  hosts:
  - minha-app.com
  http:
  - route:
    - destination:
        host: service-v1
        weight: 90
    - destination:
        host: service-v2
        weight: 10
```

### Gateway
Configura o balanceador de carga na borda do cluster para receber tráfego externo (similar ao que vimos na [[Gateway API e HTTPRoute]]).

---

## 6. Quando usar o Istio?
- **Use se:** Você tem muitos microserviços, precisa de segurança mTLS obrigatória ou precisa de controle refinado de tráfego.
- **Evite se:** Seu cluster é pequeno ou você está apenas começando. O Istio adiciona consumo de CPU/Memória e complexidade operacional considerável.

---
*Links relacionados:*
- [[Objetos Fundamentais]]
- [[Gateway API e HTTPRoute]]
- [[Monitoramento de Nodes e Pods]]
