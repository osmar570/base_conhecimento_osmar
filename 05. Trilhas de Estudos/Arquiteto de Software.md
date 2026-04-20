# Trilha de Estudos: Arquiteto de Software

O Arquiteto de Software é responsável por definir a estrutura técnica do sistema, tomar decisões difíceis (trade-offs) e garantir que a aplicação seja escalável, manutenível e segura.

---

## 🏗️ Fase 1: Design de Código e Princípios (Micro-Arquitetura)
Antes de desenhar sistemas complexos, é preciso dominar a qualidade do código.
1.  **SOLID:** A base para qualquer código orientado a objetos de qualidade.
    - [[02. Engenharia de Software/SOLID/SOLID|Guia de SOLID]]
2.  **Design Patterns:** Padrões comprovados para problemas recorrentes.
    - [[02. Engenharia de Software/Design Patterns/Design Patterns|Catálogo de Design Patterns]]

## 🏛️ Fase 2: Padrões Arquiteturais (Macro-Arquitetura)
Como organizar o sistema como um todo.
1.  **Clean Architecture:** Separação de conceitos e regra da dependência.
    - [[02. Engenharia de Software/Clean Architecture/Clean Architecture|Guia de Clean Architecture]]
2.  **Arquitetura Hexagonal:** Portas e Adaptadores para isolar o core do sistema.
    - [[02. Engenharia de Software/Clean Architecture/Diferença entre Clean vs Hexagonal|Clean vs Hexagonal]]

## 🛰️ Fase 3: Sistemas Distribuídos e Comunicação
Arquitetos precisam saber como as partes do sistema conversam.
1.  **Design de APIs:** REST, gRPC e GraphQL. Escolher o protocolo certo.
    - [[02. Engenharia de Software/Design de APIs|Design de APIs]]
    - [[02. Engenharia de Software/Tipos de APIs|Comparativo entre Protocolos]]
2.  **Event-Driven:** Mensageria e Pub/Sub (fundamental para desacoplamento).
    - [[02. Engenharia de Software/Design Patterns/Comportamentais/Observer|Padrão Observer (Base para eventos)]]

## 📊 Fase 4: Estratégia de Dados
Escolher como e onde os dados vivem.
1.  **Teorema CAP:** Entender Consistência vs Disponibilidade.
    - [[02. Engenharia de Software/Bancos de Dados|Teorema CAP e SQL vs NoSQL]]
2.  **Consistência Eventual:** Como lidar com dados em sistemas distribuídos.

## ☁️ Fase 5: Cloud-Native e Operações
A arquitetura deve sobreviver ao ambiente de execução.
1.  **Observabilidade:** Garantir que o sistema seja "auditável" internamente.
    - [[03. Plataforma e Cloud-Native/Observabilidade e SRE|SRE e Observabilidade]]
2.  **Infraestrutura como Código:** O arquiteto deve desenhar a infra junto com o código.
    - [[03. Plataforma e Cloud-Native/03. Plataforma e Cloud-Native|Plataforma e Cloud-Native]]

## 🧠 Fase 6: Decisão e Documentação
1.  **ADRs (Architecture Decision Records):** Documentar o "porquê" das decisões técnicas.
2.  **Gestão de Dívida Técnica:** Saber quando sacrificar qualidade por tempo e como pagar isso depois.

---
### 📚 Livros Recomendados:
- *Clean Architecture* (Robert C. Martin)
- *Designing Data-Intensive Applications* (Martin Kleppmann)
- *Building Microservices* (Sam Newman)
