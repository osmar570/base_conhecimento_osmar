# LSP - Liskov Substitution Principle (Princípio da Substituição de Liskov)

> "Classes derivadas devem ser substituíveis por suas classes base sem alterar a correção do programa."

Se a classe `A` é um subtipo de `B`, então os objetos do tipo `B` podem ser substituídos por objetos do tipo `A` sem que o comportamento esperado mude.

---

## ❌ Violação (Antes)
O clássico exemplo do Quadrado e Retângulo.

```csharp
public class Rectangle {
    public virtual int Width { get; set; }
    public virtual int Height { get; set; }
}

public class Square : Rectangle {
    public override int Width { set => base.Width = base.Height = value; }
    public override int Height { set => base.Height = base.Width = value; }
}
```
*   **Problema:** Se um código espera um `Rectangle` e altera a largura, ele espera que a altura permaneça a mesma. No `Square`, mudar a largura muda a altura silenciosamente, quebrando a lógica de quem o utiliza como se fosse um retângulo genérico.

## ✅ Aplicação (Depois)
Evitar herança por "conveniência" se o comportamento não for idêntico. Use interfaces mais específicas.

```csharp
public interface IShape {
    double Area();
}

public class Rectangle : IShape {
    public int Width { get; set; }
    public int Height { get; set; }
    public double Area() => Width * Height;
}

public class Square : IShape {
    public int Side { get; set; }
    public double Area() => Side * Side;
}
```
*   **Benefício:** Agora, qualquer classe que use `IShape` pode chamar `Area()` sem se preocupar com efeitos colaterais inesperados nas propriedades de largura e altura.

---
**Links Relacionados:**
- [[SOLID]] (Visão Geral)
- [[Estratégia de Testes]] (LSP garante que testes escritos para a classe pai também valem para a filha)
