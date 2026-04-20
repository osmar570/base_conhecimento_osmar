# State (Estado)

> "Permite que um objeto altere seu comportamento quando seu estado interno muda."

O **State** evita grandes blocos de `switch(state)` ou `if/else` dentro do objeto. Cada estado é encapsulado em sua própria classe, tornando as transições e o comportamento de cada fase muito mais claros.

---

## ✅ Exemplo: Pedido de E-commerce (C#)

```csharp
public interface IOrderState {
    void Next(Order order);
}

// Estados Concretos
public class NewOrder : IOrderState {
    public void Next(Order order) {
        Console.WriteLine("Pagamento confirmado.");
        order.State = new PaidOrder();
    }
}

public class PaidOrder : IOrderState {
    public void Next(Order order) {
        Console.WriteLine("Pedido enviado.");
        order.State = new ShippedOrder();
    }
}

public class ShippedOrder : IOrderState {
    public void Next(Order order) => Console.WriteLine("Pedido já entregue.");
}

// Contexto
public class Order {
    public IOrderState State { get; set; } = new NewOrder();
    public void Advance() => State.Next(this);
}

// Uso:
Order myOrder = new Order();
myOrder.Advance(); // Vira Paid
myOrder.Advance(); // Vira Shipped
```

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[SRP - Single Responsibility Principle]] (Cada estado cuida apenas da sua lógica)
