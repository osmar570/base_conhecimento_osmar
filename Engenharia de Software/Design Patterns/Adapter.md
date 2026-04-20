# Adapter (Adaptador)

> "Converte a interface de uma classe em outra interface esperada pelo cliente."

O **Adapter** permite que classes com interfaces incompatíveis trabalhem juntas. É a base da **Arquitetura Hexagonal** (Ports and Adapters), permitindo que seu sistema converse com bibliotecas de terceiros sem se acoplar a elas.

---

## ✅ Exemplo: Sistema de Pagamento Legado (C#)

```csharp
// Interface esperada pelo novo sistema
public interface ITarget {
    void RequestPayment(double amount);
}

// Classe legada (incompatível)
public class OldPaymentSystem {
    public void Pay(string value) => Console.WriteLine($"Pagando R$ {value} via sistema legado.");
}

// Adaptador
public class PaymentAdapter : ITarget {
    private readonly OldPaymentSystem _oldSystem;

    public PaymentAdapter(OldPaymentSystem oldSystem) {
        _oldSystem = oldSystem;
    }

    public void RequestPayment(double amount) {
        // Converte o tipo de dado e o método
        string valueStr = amount.ToString("F2");
        _oldSystem.Pay(valueStr);
    }
}

// Uso:
ITarget processor = new PaymentAdapter(new OldPaymentSystem());
processor.RequestPayment(150.50);
```

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[Clean Architecture]] (O Adapter isola o core da infraestrutura)
- [[ISP - Interface Segregation Principle]] (Cria interfaces que o cliente realmente usa)
