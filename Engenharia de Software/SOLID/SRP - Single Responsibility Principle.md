# SRP - Single Responsibility Principle (Princípio da Responsabilidade Única)

> "Uma classe deve ter um, e apenas um, motivo para mudar."

O SRP afirma que cada módulo ou classe deve ser responsável por **uma única parte da funcionalidade** fornecida pelo software, e essa responsabilidade deve ser inteiramente encapsulada pela classe.

---

## ❌ Violação (Antes)
Uma classe `UserService` que gerencia os dados do usuário e também lida com o envio de e-mails e logs.

```csharp
public class UserService {
    public void RegisterUser(string email) {
        // Lógica de registro no banco de dados
        Database.Save(email);

        // Lógica de envio de e-mail (Violação!)
        var emailClient = new SmtpClient();
        emailClient.Send("Bem-vindo!", email);

        // Lógica de log (Violação!)
        File.WriteAllText("log.txt", $"Usuário {email} registrado.");
    }
}
```
*   **Problema:** Se o servidor de e-mail mudar de SMTP para uma API REST, a classe `UserService` precisa ser alterada. Se o formato do log mudar, a classe `UserService` precisa ser alterada. Ela tem muitos motivos para mudar.

## ✅ Aplicação (Depois)
Dividimos as responsabilidades em classes distintas.

```csharp
public class UserService {
    private readonly IEmailService _emailService;
    private readonly ILogger _logger;

    public UserService(IEmailService emailService, ILogger logger) {
        _emailService = emailService;
        _logger = logger;
    }

    public void RegisterUser(string email) {
        Database.Save(email); // Responsabilidade central
        _emailService.SendWelcomeEmail(email); // Delegação
        _logger.Log($"Usuário {email} registrado."); // Delegação
    }
}
```
*   **Benefício:** Agora, se o envio de e-mail mudar, alteramos apenas o `EmailService`. A classe `UserService` permanece intacta.

---
**Links Relacionados:**
- [[SOLID]] (Visão Geral)
- [[Estratégia de Testes]] (Classes SRP são muito mais fáceis de testar em isolamento)
