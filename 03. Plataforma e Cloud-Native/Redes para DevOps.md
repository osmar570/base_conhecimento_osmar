# Redes para DevOps

Dominar redes é fundamental para gerenciar clusters, configurar Ingress Controllers e garantir a segurança do tráfego entre serviços. Em Cloud-Native, o foco muda do hardware para o **Software Defined Networking (SDN)**.

---

## 🌍 Protocolos Essenciais

- **TCP/UDP:** A base da comunicação. TCP garante a entrega (ex: APIs), UDP foca em velocidade (ex: Streaming, Logs).
- **HTTP/HTTPS (L7):** Protocolo de aplicação. O DevOps deve dominar Verbos, Headers e Status Codes.
- **gRPC (HTTP/2):** Protocolo binário de alta performance, padrão para comunicação *East-West* (interna) em microserviços.

---

## 🏗️ Infraestrutura e Roteamento

### 1. DNS (Domain Name System)
O "catálogo telefônico" da internet.
- **Registros comuns:** `A` (IPv4), `CNAME` (Apelido), `TXT` (Verificação), `SRV` (Serviços).
- **CoreDNS:** O servidor de DNS padrão dentro do Kubernetes que resolve nomes de serviços (ex: `meu-servico.namespace.svc.cluster.local`).

### 2. Load Balancers e Proxies
- **L4 Load Balancer:** Balanceia tráfego baseado em IP e Porta (TCP/UDP). Rápido, mas não lê o conteúdo da requisição.
- **L7 Load Balancer (Ingress):** Balanceia baseado na URL, Path ou Headers. Essencial para rotear múltiplos serviços em um único IP.
- **Reverse Proxy (Nginx/Envoy):** Recebe a requisição e a repassa para o serviço interno, provendo segurança e cache.

---

## 🔐 Segurança e Criptografia

### TLS/SSL (HTTPS)
- **Handshake:** O processo de negociar chaves seguras entre cliente e servidor.
- **Certificados:** Emitidos por CAs (Certificate Authorities) como Let's Encrypt.
- **mTLS (Mutual TLS):** Tanto o cliente quanto o servidor apresentam certificados. É o padrão de segurança para **Service Mesh** (Istio/Linkerd).

---

## ☸️ Redes no Kubernetes (Resumo)

1.  **Pod Networking:** Cada Pod tem seu próprio IP único no cluster.
2.  **Service (ClusterIP):** Um IP virtual estável que balanceia o tráfego para um grupo de Pods.
3.  **Ingress Controller:** O ponto de entrada do tráfego externo para o cluster.
4.  **Network Policies:** O "Firewall" do Kubernetes que define quais Pods podem falar com quais Pods.

---
**Links Relacionados:**
- [[03. Plataforma e Cloud-Native/Kubernetes/Kubernetes|Guia de Kubernetes]]
- [[03. Plataforma e Cloud-Native/Kubernetes/Gateway API e HTTPRoute|A Evolução do Roteamento]]
- [[01. Fundamentos/Linux/Redes no Linux|Comandos de Rede no Linux]]
