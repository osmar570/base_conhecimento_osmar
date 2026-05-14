# Service Mesh (Malha de Serviços)

Uma Service Mesh é uma camada de infraestrutura dedicada para gerenciar a comunicação entre serviços (East-West traffic) de forma segura, rápida e confiável.

## 🧱 Arquitetura
A maioria das Service Meshes utiliza o padrão de **Sidecar Proxy**:
* **Data Plane**: Proxies leves (como o Envoy) injetados junto a cada microserviço para interceptar o tráfego.
* **Control Plane**: O cérebro que gerencia as configurações, políticas de segurança e certificados dos proxies.

## 🚀 Funcionalidades Principais
1. **Gerenciamento de Tráfego**: Retries, Timeouts, Circuit Breaking e Canary Deployments.
2. **Segurança**: Criptografia mTLS automática entre todos os serviços e políticas de autorização granulares.
3. **Observabilidade**: Geração automática de métricas (Douradas), logs de acesso e tracing distribuído sem alterar o código da aplicação.

## ⚖️ Istio vs Linkerd
| Característica | Istio | Linkerd |
| :--- | :--- | :--- |
| **Complexidade** | Alta (Muitos recursos) | Baixa (Foco em simplicidade) |
| **Performance** | Pode ter overhead maior | Extremamente leve (escrito em Rust) |
| **Ecossistema** | Muito robusto, padrão de fato | Focado no CNCF, muito amigável |
| **Configuração** | Baseada em CRDs complexos | Minimalista |

## 🛠️ Quando Usar?
* **Use**: Se você tem uma arquitetura de microserviços complexa, precisa de mTLS obrigatório por compliance ou precisa de controle de tráfego avançado.
* **Não Use**: Se sua aplicação é monolítica ou tem poucos serviços; a complexidade operacional pode não valer o benefício.

---
**Links Relacionados:**
- [[Kubernetes/Service Mesh - Istio|Detalhes Técnicos: Istio]]
