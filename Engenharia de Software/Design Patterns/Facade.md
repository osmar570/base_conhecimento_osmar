# Facade (Fachada)

> "Fornece uma interface simplificada para um conjunto complexo de classes em um subsistema."

O **Facade** esconde a complexidade de um sistema interno (composto de muitas classes e dependências) e expõe apenas o que é essencial para o cliente.

---

## ✅ Exemplo: Sistema de Pedidos (C#)

```csharp
// Subsistemas complexos
public class Inventory { public bool Check() => true; }
public class Payment { public bool Process() => true; }
public class Shipping { public void Ship() => Console.WriteLine("Enviando..."); }

// Fachada (Facade) simplifica o uso de todos eles
public class OrderFacade {
    private readonly Inventory _inv = new Inventory();
    private readonly Payment _pay = new Payment();
    private readonly Shipping _ship = new Shipping();

    public void PlaceOrder() {
        if (_inv.Check() && _pay.Process()) {
            _ship.Ship();
            Console.WriteLine("Pedido Finalizado!");
        }
    }
}

// Uso simples:
OrderFacade order = new OrderFacade();
order.PlaceOrder(); // O cliente não precisa conhecer Inventory, Payment ou Shipping
```

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[Clean Architecture]] (O Facade ajuda a expor Use Cases de forma simples)
