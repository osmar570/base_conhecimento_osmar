# Autenticação e Segurança de Aplicação

Garantir que apenas usuários e sistemas autorizados acessem recursos protegidos é um pilar crítico do desenvolvimento de software. Em arquiteturas distribuídas e APIs, o uso de padrões abertos é mandatário.

---

## 🔐 Autenticação vs. Autorização

- **Autenticação (AuthN):** "Quem é você?". O processo de verificar a identidade (ex: login com senha, biometria).
- **Autorização (AuthZ):** "O que você pode fazer?". O processo de verificar permissões (ex: um usuário comum não pode deletar outros usuários).

---

## 🎫 JWT (JSON Web Token)

O JWT é um padrão (RFC 7519) para transmitir informações de forma compacta e segura como um objeto JSON.
- **Header:** Tipo de token e algoritmo de criptografia.
- **Payload (Claims):** Dados do usuário e permissões (não deve conter segredos, pois é apenas codificado, não criptografado).
- **Signature:** Garante que o token não foi alterado no caminho.

---

## 🚀 Protocolos Modernos

### 1. OAuth 2.0 (Framework de Autorização)
Permite que uma aplicação obtenha acesso limitado a uma conta de usuário em outro serviço (ex: "Login com Google").
- **Roles:** Resource Owner, Client, Authorization Server, Resource Server.
- **Tokens:** Access Token (curta duração) e Refresh Token (longa duração).

### 2. OIDC - OpenID Connect (Camada de Identidade)
Uma camada sobre o OAuth 2.0 que adiciona informações sobre o usuário autenticado.
- Introduz o **ID Token**, que contém informações do perfil do usuário.

---

## 🛡️ Boas Práticas de Segurança em APIs

- **HTTPS Everywhere:** Nunca transmita tokens ou credenciais em texto claro.
- **Princípio do Menor Privilégio:** Conceda apenas as permissões necessárias para a tarefa.
- **Validação de Input:** Proteja-se contra SQL Injection e XSS.
- **Rate Limiting:** Evite ataques de força bruta e negação de serviço (DoS).
- **Secrets Management:** Nunca versionar chaves de API ou segredos no Git. Use Vaults ou Environment Variables.

---
**Links Relacionados:**
- [[02. Engenharia de Software/Design de APIs|Design de APIs]] (Onde a segurança é aplicada)
- [[03. Plataforma e Cloud-Native/Docker/Segurança no Docker|Segurança na Infraestrutura]]
- [[05. Trilhas de Estudos/Desenvolvedor CSharp - Pleno|Trilha Pleno]] (Requisito de carreira)
