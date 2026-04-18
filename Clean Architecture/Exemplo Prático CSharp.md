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

## ⚖️ Value Object vs DTO (Diferenças Cruciais)

Embora ambos pareçam "classes de dados" simples, eles vivem em camadas diferentes e possuem propósitos opostos na Clean Architecture.

### 1. Value Object (Objeto de Valor)
*   **Onde vive:** Camada de **Domain**.
*   **O que é:** Um objeto que não possui identidade própria (ID). Ele é definido pela totalidade de seus atributos.
*   **Características:** 
    *   **Imutável:** Uma vez criado, seus valores não mudam. Se precisar mudar, você cria um novo objeto.
    *   **Igualdade por valor:** Dois objetos de Endereço são iguais se todas as ruas e números forem iguais.
    *   **Lógica de Negócio:** Pode e deve conter validações (ex: um `CPF` que se valida na criação).

### 2. DTO (Data Transfer Object)
*   **Onde vive:** Camadas de **Application** ou **WebAPI**.
*   **O que é:** Uma "sacola de dados" usada apenas para transportar informações de um lugar para outro (ex: da API para o Caso de Uso).
*   **Características:**
    *   **Anêmico:** Não possui nenhuma lógica de negócio.
    *   **Estrutura Plana:** Geralmente contém apenas propriedades simples (strings, ints) para facilitar a serialização (JSON).
    *   **Contrato:** Define o que o cliente da API deve enviar ou o que ele vai receber.

### Comparativo Rápido

| Característica | Value Object | DTO |
| :--- | :--- | :--- |
| **Camada** | Domain | Application / WebAPI |
| **Lógica** | Sim (Validação/Negócio) | Não (Apenas dados) |
| **Mudança** | Imutável | Mutável (geralmente) |
| **Finalidade** | Representar um conceito do negócio | Transportar dados entre camadas |

---
**Links Relacionados:**
- [[Clean Architecture]]
- [[Regra da Dependência e DIP]]
- [[Interface Adapters (Controllers e Gateways)]]
