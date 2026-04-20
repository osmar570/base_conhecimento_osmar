# ISP - Interface Segregation Principle (Princípio da Segregação de Interface)

> "Nenhum cliente deve ser forçado a depender de métodos que não utiliza."

É melhor ter várias interfaces específicas e pequenas do que uma única interface genérica e "pesada".

---

## ❌ Violação (Antes)
Uma interface gigante para máquinas de escritório.

```csharp
public interface IMachine {
    void Print();
    void Scan();
    void Fax();
}

public class SimplePrinter : IMachine {
    public void Print() => // Imprime...
    public void Scan() => throw new NotImplementedException(); // Violação!
    public void Fax() => throw new NotImplementedException(); // Violação!
}
```
*   **Problema:** A `SimplePrinter` é forçada a implementar métodos que não suporta, apenas para satisfazer o contrato da interface. Isso gera código frágil e exceções em tempo de execução.

## ✅ Aplicação (Depois)
Dividir a interface grande em interfaces menores e específicas.

```csharp
public interface IPrinter {
    void Print();
}

public interface IScanner {
    void Scan();
}

public class SimplePrinter : IPrinter {
    public void Print() => // Imprime...
}

public class MultiFunctionPrinter : IPrinter, IScanner {
    public void Print() => // Imprime...
    public void Scan() => // Escaneia...
}
```
*   **Benefício:** As classes dependem apenas do que realmente precisam. Se você mudar a interface `IScanner`, a `SimplePrinter` nem fica sabendo e não precisa ser recompilada.

---
**Links Relacionados:**
- [[SOLID]] (Visão Geral)
- [[Design Patterns]] (O padrão **Adapter** ajuda a cumprir o ISP ao adaptar interfaces legadas)
