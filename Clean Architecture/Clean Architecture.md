# Clean Architecture (Arquitetura Limpa)

A **Clean Architecture** é um paradigma de design de software popularizado por Robert C. Martin (Uncle Bob). Seu objetivo principal é a **separação de preocupações**, permitindo que o código seja testável, independente de frameworks, interface de usuário ou banco de dados.

## 1. O Princípio da Dependência

A regra de ouro da Clean Architecture é: **As dependências de código só podem apontar para dentro.**
O núcleo do software (as regras de negócio) não deve conhecer nada sobre o mundo exterior (banco de dados, APIs externas, UI).

## 2. As Camadas (O Diagrama de Cebola)

Uma implementação padrão geralmente é dividida em:

1.  **Entities (Entidades):** Regras de negócio corporativas (ex: uma classe `Cliente` com validações).
2.  **Use Cases (Casos de Uso):** Regras de negócio específicas da aplicação (ex: `RealizarVenda`, `CadastrarUsuario`).
3.  **Interface Adapters (Adaptadores):** Convertem dados dos Casos de Uso para o formato mais conveniente para frameworks externos (ex: Controllers, Presenters, Gateways).
4.  **Frameworks & Drivers:** Onde ficam as ferramentas externas (Express.js, MongoDB, React, etc.).

## 🗺️ Trilha de Aprendizagem em Clean Architecture

Para dominar este assunto, vamos construir o conhecimento nesta ordem:

1.  **Fundamentos:** Entender o porquê de usar arquitetura limpa e o custo da dívida técnica (esta nota).
2.  **A Regra da Dependência:** Como usar Inversão de Dependência (DIP) para proteger o núcleo.
3.  **Camadas em Detalhes:** Explorar Entidades, Casos de Uso e Adaptadores.
4.  **Diferença entre Clean vs Hexagonal:** Comparativo entre arquiteturas similares.
5.  **Exemplos Práticos:** Implementação de uma API usando estes conceitos.

---
**Links Relacionados:**
- [[Docker]] (Como conteinerizar uma app Clean)
- [[Kubernetes]] (Escalando apps desacopladas)
