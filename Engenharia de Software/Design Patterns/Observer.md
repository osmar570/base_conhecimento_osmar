# Observer (Observador)

> "Define uma dependência um-para-muitos, notificando mudanças de estado a todos os dependentes."

O **Observer** é a base de sistemas **Event-Driven** e padrões modernos de UI. Ele permite que múltiplos objetos reajam a mudanças em um único objeto (Subject) sem que este precise conhecer seus observadores.

---

## ✅ Exemplo: Sistema de Notificações de Preço (C#)

```csharp
public interface IObserver {
    void Update(double price);
}

// O Sujeito (Subject)
public class Product {
    private List<IObserver> _observers = new List<IObserver>();
    private double _price;

    public void Attach(IObserver obs) => _observers.Add(obs);
    
    public double Price {
        get => _price;
        set {
            _price = value;
            Notify();
        }
    }

    private void Notify() {
        foreach (var obs in _observers) obs.Update(_price);
    }
}

// Observadores
public class UserApp : IObserver {
    public void Update(double price) => Console.WriteLine($"App: Novo preço: {price}");
}

// Uso:
Product tv = new Product();
tv.Attach(new UserApp());
tv.Price = 1999.00; // Notifica automaticamente
```

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[Observabilidade e SRE]] (Métricas e logs são observadores do sistema)
