# Padrões de Microserviços

A adoção de microserviços traz agilidade, mas aumenta a complexidade. O uso de padrões arquiteturais é essencial para gerenciar a consistência de dados e a comunicação entre componentes.

---

## 🏛️ Padrões de Gerenciamento de Dados

### 1. CQRS (Command Query Responsibility Segregation)
Separação da responsabilidade de escrita (Comandos) da responsabilidade de leitura (Consultas).

#### ✅ Exemplo em C# (usando MediatR)
O padrão MediatR é amplamente usado para implementar CQRS em .NET, desacoplando quem envia o comando de quem o processa.

```csharp
// 1. O Comando (Escrita)
public record CreateUserCommand(string Name, string Email) : IRequest<Guid>;

// 2. O Handler (Processador do Comando)
public class CreateUserHandler : IRequestHandler<CreateUserCommand, Guid> {
    public async Task<Guid> Handle(CreateUserCommand request, CancellationToken ct) {
        var id = Guid.NewGuid();
        // Lógica para salvar no banco de escrita (SQL Server)
        Console.WriteLine($"Usuário {request.Name} criado no banco de escrita.");
        return id;
    }
}

// 3. A Query (Leitura - Independente da escrita)
public record GetUserByIdQuery(Guid Id) : IRequest<UserDto>;
```

### 2. Event Sourcing
Em vez de armazenar o estado atual, armazenamos a **sequência de eventos**.

#### ✅ Conceito em C#
Muitas vezes implementado com bibliotecas como **Marten** ou **EventStoreDB**.
```csharp
public record UserRegistered(Guid Id, string Name, DateTime OccurredOn);
public record UserEmailUpdated(Guid Id, string NewEmail, DateTime OccurredOn);

// O estado é reconstruído aplicando a lista de eventos
public class UserAccount {
    public string Name { get; private set; }
    public void Apply(UserRegistered e) => Name = e.Name;
}
```

---

## 🛰️ Padrões de Exposição e Consumo

### 1. API Gateway
Ponto de entrada único. Em .NET, ferramentas como **Ocelot** ou **YARP** são padrão.

### 2. BFF (Backend for Frontend)
Backend específico para cada tipo de interface (Mobile, Web, IoT).

#### ✅ Exemplo em C# (Agregação simples)
```csharp
[ApiController]
[Route("mobile/order-details")]
public class OrderBffController : ControllerBase {
    private readonly IOrderService _orderService;
    private readonly ICustomerService _customerService;

    public async Task<IActionResult> Get(Guid orderId) {
        // BFF agrega dados de múltiplos serviços para otimizar o payload do Mobile
        var order = await _orderService.GetById(orderId);
        var customer = await _customerService.GetById(order.CustomerId);
        
        return Ok(new { order.Total, customer.Name, order.Status });
    }
}
```

---

## 🔄 Resiliência e Consistência

### 1. Circuit Breaker
Impede que falhas em cascata derrubem o sistema.

#### ✅ Exemplo em C# (usando Polly)
```csharp
var circuitBreakerPolicy = Policy
    .Handle<HttpRequestException>()
    .CircuitBreakerAsync(
        exceptionsAllowedBeforeBreaking: 3,
        durationOfBreak: TimeSpan.FromSeconds(30)
    );

// Uso
await circuitBreakerPolicy.ExecuteAsync(() => _httpClient.GetAsync("https://api-externa.com"));
```

### 2. Saga Pattern
Gerencia transações distribuídas (Saga Orquestrada ou Coreografada).
- **C# Way:** Em .NET, o **MassTransit** é a ferramenta líder para implementar Sagas através de *State Machines*.

---
**Links Relacionados:**
- [[02. Engenharia de Software/Mensageria e Eventos|Mensageria e Eventos]] (O transporte para CQRS e Sagas)
- [[02. Engenharia de Software/Clean Architecture/Clean Architecture|Clean Architecture]] (Organização interna de cada microserviço)
- [[05. Trilhas de Estudos/Arquiteto de Software|Trilha de Arquiteto]] (Decisões de macro-arquitetura)
