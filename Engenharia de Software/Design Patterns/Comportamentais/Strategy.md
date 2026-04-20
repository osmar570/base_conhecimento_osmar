# Strategy (Estratégia)

> "Define uma família de algoritmos, encapsula cada um e os torna intercambiáveis."

O **Strategy** permite que o algoritmo mude independentemente dos clientes que o utilizam, evitando grandes blocos de `if/else` ou `switch` no código.

---

## ✅ Exemplo: Métodos de Pagamento (C#)

```csharp
public interface IPaymentStrategy {
    void Pay(double amount);
}

// Estratégia Cartão
public class CreditCardPayment : IPaymentStrategy {
    public void Pay(double amount) => Console.WriteLine($"Pago R$ {amount} no Cartão.");
}

// Estratégia Pix
public class PixPayment : IPaymentStrategy {
    public void Pay(double amount) => Console.WriteLine($"Pago R$ {amount} via Pix.");
}

// O Contexto
public class ShoppingCart {
    public void Process(double amount, IPaymentStrategy strategy) {
        strategy.Pay(amount);
    }
}

// Uso:
ShoppingCart cart = new ShoppingCart();
cart.Process(100.00, new PixPayment());
```

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[OCP - Open-Closed Principle]] (O Strategy é a implementação do OCP)
