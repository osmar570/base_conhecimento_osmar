# DIP - Dependency Inversion Principle (Princípio da Inversão de Dependência)

> "Dependa de abstrações e não de implementações concretas."

1. Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações.
2. Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações.

---

## ❌ Violação (Antes)
Uma classe de alto nível criando instâncias de classes de baixo nível internamente.

```csharp
public class NotificationService {
    private readonly EmailSender _emailSender = new EmailSender();

    public void Send(string msg) {
        _emailSender.SendEmail(msg);
    }
}
```
*   **Problema:** `NotificationService` está fortemente acoplado ao `EmailSender`. Se quisermos trocar para `SmsSender`, temos que modificar o serviço de notificação.

## ✅ Aplicação (Depois)
Injetar a dependência através de uma interface.

```csharp
public interface IMessageSender {
    void Send(string message);
}

public class EmailSender : IMessageSender {
    public void Send(string message) => // Envia E-mail...
}

public class NotificationService {
    private readonly IMessageSender _sender;

    public NotificationService(IMessageSender sender) {
        _sender = sender;
    }

    public void Send(string msg) {
        _sender.Send(msg);
    }
}
```
*   **Benefício:** `NotificationService` não sabe (e nem se importa) como a mensagem é enviada. Isso facilita testes unitários (usando **Mocks**) e permite trocar a forma de envio sem tocar no código de alto nível.

---
**Links Relacionados:**
- [[SOLID]] (Visão Geral)
- [[Clean Architecture]] (O DIP é a base da Regra da Dependência)
- [[Estratégia de Testes]] (DIP permite o uso de Dublês de Teste)
