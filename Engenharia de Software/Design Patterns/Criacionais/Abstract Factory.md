# Abstract Factory (Fábrica Abstrata)

> "Fornece uma interface para criar famílias de objetos relacionados sem especificar suas classes concretas."

Diferente do **Factory Method**, que cria apenas um tipo de objeto, o **Abstract Factory** lida com a criação de **famílias** de objetos que precisam trabalhar juntos.

---

## ✅ Exemplo: UI Multiplataforma (C#)
Imagine que sua aplicação precisa criar botões e campos de texto que tenham o visual do Windows ou do macOS.

```csharp
// Produtos abstratos
public interface IButton { void Render(); }
public interface ITextField { void Render(); }

// Produtos concretos para Windows
public class WinButton : IButton { public void Render() => Console.WriteLine("Botão Windows"); }
public class WinTextField : ITextField { public void Render() => Console.WriteLine("Campo Windows"); }

// Produtos concretos para macOS
public class MacButton : IButton { public void Render() => Console.WriteLine("Botão Mac"); }
public class MacTextField : ITextField { public void Render() => Console.WriteLine("Campo Mac"); }

// Fábrica abstrata
public interface IUIFactory {
    IButton CreateButton();
    ITextField CreateTextField();
}

// Fábricas concretas
public class WindowsFactory : IUIFactory {
    public IButton CreateButton() => new WinButton();
    public ITextField CreateTextField() => new WinTextField();
}

public class MacFactory : IUIFactory {
    public IButton CreateButton() => new MacButton();
    public ITextField CreateTextField() => new MacTextField();
}

// Uso:
IUIFactory factory = new WindowsFactory();
var button = factory.CreateButton();
button.Render();
```

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[Factory Method]] (Diferença: um objeto vs família de objetos)
