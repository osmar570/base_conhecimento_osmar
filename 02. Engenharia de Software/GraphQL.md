# GraphQL

GraphQL é uma linguagem de consulta para APIs e um runtime para executar essas consultas usando um sistema de tipos definido para seus dados.

## 🚀 Conceitos Fundamentais
* **Schema**: O contrato que define os tipos de dados, queries e mutations disponíveis.
* **Query**: Solicitação de dados específicos (resolve o problema de *over-fetching* e *under-fetching*).
* **Mutation**: Operações para criar, atualizar ou deletar dados.
* **Subscription**: Comunicação em tempo real via WebSockets para ouvir mudanças nos dados.
* **Resolvers**: Funções no servidor que buscam os dados para cada campo no schema.

## ⚖️ REST vs GraphQL
| Característica | REST | GraphQL |
| :--- | :--- | :--- |
| **Busca de Dados** | Múltiplos endpoints, estrutura fixa | Endpoint único, estrutura flexível |
| **Tipagem** | Fraca (geralmente JSON) | Forte (Schema Definition Language) |
| **Performance** | Cache HTTP nativo | Cache mais complexo (geralmente no cliente) |
| **Versão** | Geralmente via URL (v1, v2) | Evolução contínua sem versionamento de URL |

## 🛠️ Ferramentas Populares
* **Apollo Server/Client**: A stack mais popular para JS/TS.
* **Hot Chocolate**: Implementação robusta para .NET.
* **GraphiQL / Apollo Studio**: Ferramentas de exploração e teste de APIs.
