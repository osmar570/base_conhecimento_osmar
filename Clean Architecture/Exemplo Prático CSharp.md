# Exemplo Prático de Estrutura em C# (.NET)

Em C#, a [[Clean Architecture]] é implementada dividindo o sistema em diferentes projetos para garantir que as dependências de referência apontem apenas para o núcleo.

## 📁 Estrutura da Solution (.sln)

```text
MinhaApp.sln
├── src/
│   ├── MinhaApp.Domain/            (Camada Interna - Entities)
│   ├── MinhaApp.Application/       (Camada Interna - Use Cases)
│   ├── MinhaApp.Infrastructure/    (Camada Externa - DB, APIs)
│   └── MinhaApp.WebAPI/            (Camada Externa - Controllers)
└── tests/
    ├── MinhaApp.UnitTests/
    └── MinhaApp.IntegrationTests/
```

---

## 🏗️ Responsabilidades de cada Pasta/Projeto

### 1. `MinhaApp.Domain` (Coração do Sistema)
*   **Responsabilidade:** Contém as regras de negócio puras (Entities) e as interfaces (Contratos).
*   **O que tem dentro:**
    *   `Entities/`: Classes como `Pedido.cs`, `Cliente.cs` com validações.
    *   `Interfaces/`: Definições como `IPedidoRepository.cs`.
    *   `ValueObjects/`: Objetos como `Endereco.cs` ou `CPF.cs`.
*   **Dependências:** **ZERO**. Não referencia nenhum outro projeto.

### 2. `MinhaApp.Application` (Casos de Uso)
*   **Responsabilidade:** Implementa os processos do sistema, orquestrando as entidades.
*   **O que tem dentro:**
    *   `UseCases/`: Classes como `CriarPedidoUseCase.cs` ou `FinalizarCompraHandler.cs`.
    *   `DTOs/`: Objetos de entrada e saída (Request/Response).
    *   `Validators/`: Regras específicas do fluxo (ex: FluentValidation).
*   **Dependências:** Referencia apenas o `Domain`.

### 3. `MinhaApp.Infrastructure` (Adaptadores de Saída)
*   **Responsabilidade:** Implementa a persistência e a comunicação com o mundo externo.
*   **O que tem dentro:**
    *   `Persistence/`: Implementação do Entity Framework (`AppDbContext.cs`), Migrations e Repositories reais.
    *   `ExternalServices/`: Integração com Gateways de Pagamento, Envio de E-mail (SendGrid), etc.
*   **Dependências:** Referencia `Domain` e `Application` (para implementar as interfaces).

### 4. `MinhaApp.WebAPI` (Adaptadores de Entrada)
*   **Responsabilidade:** O ponto de entrada da aplicação (Entry Point).
*   **O que tem dentro:**
    *   `Controllers/`: Recebem o tráfego HTTP e chamam os Casos de Uso.
    *   `Configuration/`: Injeção de Dependência (Dependency Injection), Auth e Middlewares.
    *   `Program.cs`: Inicialização do sistema.
*   **Dependências:** Referencia `Application` e `Infrastructure` (apenas para configurar a Injeção de Dependência na inicialização).

---

## 🛠️ Exemplo de Fluxo de Injeção
No C#, no arquivo `Program.cs`, você "amarra" tudo:
```csharp
// Diz que quando alguém pedir IPedidoRepository (Domain), 
// o sistema deve dar o SqlPedidoRepository (Infrastructure).
builder.Services.AddScoped<IPedidoRepository, SqlPedidoRepository>();

// Registra os Casos de Uso
builder.Services.AddScoped<ICriarPedidoUseCase, CriarPedidoUseCase>();
```

---
**Links Relacionados:**
- [[Clean Architecture]]
- [[Regra da Dependência e DIP]]
- [[Interface Adapters (Controllers e Gateways)]]
