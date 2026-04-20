# OCP - Open-Closed Principle (Princípio Aberto-Fechado)

> "Entidades de software devem estar abertas para extensão, mas fechadas para modificação."

Você deve ser capaz de adicionar novas funcionalidades a um sistema sem precisar alterar o código-fonte existente que já está funcionando e testado.

---

## ❌ Violação (Antes)
Uma classe que calcula descontos baseada em tipos fixos usando `if` ou `switch`.

```csharp
public class DiscountCalculator {
    public double Calculate(double amount, string type) {
        if (type == "VIP") return amount * 0.8;
        if (type == "BlackFriday") return amount * 0.5;
        return amount;
    }
}
```
*   **Problema:** Toda vez que um novo tipo de desconto for criado (ex: Natal), você precisa **modificar** a classe `DiscountCalculator`, o que pode introduzir bugs no código que já funcionava.

## ✅ Aplicação (Depois)
Usamos abstrações (Interfaces ou Classes Abstratas) para permitir extensão via polimorfismo.

```csharp
public interface IDiscountStrategy {
    double ApplyDiscount(double amount);
}

public class VipDiscount : IDiscountStrategy {
    public double ApplyDiscount(double amount) => amount * 0.8;
}

public class BlackFridayDiscount : IDiscountStrategy {
    public double ApplyDiscount(double amount) => amount * 0.5;
}

public class DiscountCalculator {
    public double Calculate(double amount, IDiscountStrategy strategy) {
        return strategy.ApplyDiscount(amount);
    }
}
```
*   **Benefício:** Se quisermos adicionar um desconto de Natal, basta criar uma nova classe `ChristmasDiscount` que implementa a interface. A classe `DiscountCalculator` permanece **fechada para modificação**.

---
**Links Relacionados:**
- [[SOLID]] (Visão Geral)
- [[Design Patterns]] (O padrão **Strategy** é a aplicação pura do OCP)
