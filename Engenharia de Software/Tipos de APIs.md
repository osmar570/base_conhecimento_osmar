# Tipos de APIs: REST, gRPC e GraphQL

A escolha da arquitetura de API impacta diretamente a performance, a facilidade de desenvolvimento e a escalabilidade do sistema. Cada modelo resolve problemas específicos de comunicação.

---

## 🌐 1. REST (Representational State Transfer)
O padrão mais comum na web, baseado nos princípios do protocolo HTTP.

- **Modelo:** Orientado a Recursos (Resources).
- **Protocolo:** HTTP 1.1 / 2.
- **Formato de Dados:** Majoritariamente JSON, mas suporta XML, HTML, etc.
- **Características:**
    - **Stateless:** Cada requisição contém toda a informação necessária para ser processada.
    - **Cache nativo:** Utiliza headers HTTP (`ETag`, `Cache-Control`) para otimizar performance.
    - **Interface Uniforme:** Uso semântico dos verbos (GET, POST, PUT, DELETE).
- **Ideal para:** APIs públicas, integrações web simples e sistemas que exigem cache agressivo.

## 🚀 2. gRPC (Google Remote Procedure Call)
Um framework de alta performance que utiliza tecnologias modernas para comunicação eficiente.

- **Modelo:** Orientado a Procedimentos (RPC).
- **Protocolo:** HTTP/2 (Obrigatório).
- **Formato de Dados:** Protocol Buffers (Protobuf) - binário.
- **Características:**
    - **Performance:** O formato binário é muito menor e mais rápido de processar que o JSON.
    - **Streaming:** Suporta streaming bidirecional (cliente e servidor enviando dados simultaneamente).
    - **Tipagem Forte:** O contrato (.proto) garante que cliente e servidor falem a mesma língua.
- **Ideal para:** Comunicação entre microsserviços (East-West traffic), sistemas de baixa latência e ambientes Kubernetes.

## 🕸️ 3. GraphQL
Uma linguagem de consulta para APIs criada pelo Facebook para resolver problemas de eficiência no carregamento de dados.

- **Modelo:** Orientado a Grafos/Consultas.
- **Protocolo:** HTTP.
- **Formato de Dados:** JSON.
- **Características:**
    - **No Over-fetching:** O cliente pede exatamente os campos que precisa.
    - **Single Endpoint:** Tudo é resolvido em uma única rota (geralmente `/graphql`).
    - **Schema Declarativo:** O servidor define um esquema e o cliente navega pelas relações.
- **Ideal para:** Aplicações Mobile/Frontend complexas, agregação de múltiplos microserviços (BFF - Backend for Frontend).

---

## 📊 Comparativo Técnico

| Característica | REST | gRPC | GraphQL |
| :--- | :--- | :--- | :--- |
| **Contrato** | Opcional (OpenAPI) | Obrigatório (.proto) | Obrigatório (Schema) |
| **Protocolo** | HTTP 1.1/2 | HTTP/2 | HTTP |
| **Payload** | Texto (JSON/XML) | Binário (Protobuf) | Texto (JSON) |
| **Performance** | Média | Alta | Média/Alta |
| **Cache** | Excelente (Nativo) | Difícil | Complexo (nível de campo) |
| **Tipagem** | Fraca | Forte | Forte |

---

## ⚖️ Qual escolher?

1.  **Escolha REST** se você precisa de simplicidade, padrões web universais e cache eficiente para o público externo.
2.  **Escolha gRPC** para comunicação interna onde performance e latência são críticas (ex: entre serviços dentro do seu cluster K8s).
3.  **Escolha GraphQL** se você tem um frontend que precisa de flexibilidade para buscar dados de várias fontes e quer evitar múltiplas chamadas de API.

---
**Links Relacionados:**
- [[Design de APIs]] (Conceitos de versionamento e idempotência)
- [[Kubernetes]] (Onde gRPC brilha com HTTP/2)
- [[Estratégia de Testes]] (Testes de contrato e integração para APIs)
