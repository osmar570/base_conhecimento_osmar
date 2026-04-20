# Design de APIs

Design de APIs é a arte de criar contratos de comunicação entre sistemas que sejam intuitivos, performáticos e sustentáveis a longo prazo.

---

## 🛰️ Estilos de Comunicação

### 1. REST (Representational State Transfer)
- **Base:** Protocolo HTTP e Verbos (GET, POST, PUT, DELETE).
- **Formatos:** Majoritariamente JSON.
- **Vantagem:** Universal, fácil de testar, excelente cache HTTP.
- **Desvantagem:** Pode ser verboso (over-fetching) e não tem tipagem forte nativa.

### 2. gRPC (Google Remote Procedure Call)
- **Base:** HTTP/2 e Protocol Buffers (Protobuf).
- **Vantagem:** Extremamente rápido, tipagem forte, suporte a streaming bidirecional.
- **Desvantagem:** Difícil de testar sem ferramentas específicas; não é nativo para navegadores (precisa de gRPC-Web).
- **Uso ideal:** Comunicação interna entre microsserviços em **Kubernetes**.

---

## 🔄 Versionamento

Estratégias para evoluir a API sem quebrar os clientes existentes.
- **URI Versioning:** `/v1/resource` (Padrão de mercado pela simplicidade).
- **Header Versioning:** Usar headers customizados ou `Accept`.
- **Breaking Changes:** Mudanças que obrigam o aumento da versão major (remover campos, mudar tipos, renomear rotas).

---

## 🛡️ Idempotência
Um conceito vital para sistemas distribuídos (Cloud-Native).
- **Definição:** Uma operação é idempotente se o resultado de executá-la múltiplas vezes for o mesmo que executá-la uma única vez.
- **Verbos:** `GET`, `PUT`, `DELETE` e `HEAD` são naturalmente idempotentes.
- **O Desafio do POST:** Para tornar um `POST` idempotente (ex: criar um pedido), usa-se uma **Idempotency-Key** no header. Se o sistema cair e o cliente reenviar a mesma chave, o servidor sabe que já processou e não duplica o pedido.

---

## 📝 Documentação e Contratos
- **OpenAPI (Swagger):** O padrão para documentar APIs REST. Permite gerar clientes e servidores automaticamente.
- **Design-First:** Escrever a especificação da API antes de escrever o código. Isso garante que o contrato seja discutido e validado por todos os stakeholders.

---
**Links Relacionados:**
- [[Versão Semântica (SemVer)]] (Lógica por trás das versões v1, v2)
- [[Kubernetes]] (Onde os Ingress Controllers gerenciam o roteamento de versões)
- [[Estratégia de Testes]] (Testes de contrato para garantir que a API não quebrou)
