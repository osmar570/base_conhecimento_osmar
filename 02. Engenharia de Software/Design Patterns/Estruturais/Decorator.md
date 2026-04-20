# Decorator (Decorador)

> "Adiciona responsabilidades a um objeto dinamicamente sem alterar sua estrutura."

O **Decorator** é uma alternativa flexível à herança para estender funcionalidades. Ele permite "envelopar" um objeto com camadas adicionais de comportamento (ex: Logging, Cache, Criptografia).

---

## ✅ Exemplo: Sistema de Notificação (C#)

```csharp
public interface INotifier {
    void Send(string message);
}

// Implementação básica
public class EmailNotifier : INotifier {
    public void Send(string msg) => Console.WriteLine($"Enviando E-mail: {msg}");
}

// Decorador base
public abstract class NotifierDecorator : INotifier {
    protected INotifier _notifier;
    public NotifierDecorator(INotifier notifier) => _notifier = notifier;
    public virtual void Send(string msg) => _notifier.Send(msg);
}

// Decoradores concretos
public class SmsDecorator : NotifierDecorator {
    public SmsDecorator(INotifier n) : base(n) {}
    public override void Send(string msg) {
        base.Send(msg);
        Console.WriteLine($"Enviando SMS: {msg}");
    }
}

// Uso Dinâmico:
INotifier sender = new EmailNotifier();
sender = new SmsDecorator(sender); // Adiciona SMS ao E-mail
sender.Send("Olá!");
```

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[OCP - Open-Closed Principle]] (Extensão sem modificação do código original)
