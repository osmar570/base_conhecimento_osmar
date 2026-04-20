# Singleton

> "Garante que uma classe tenha apenas uma instância e fornece um ponto de acesso global a ela."

O **Singleton** é muito útil para gerenciar recursos compartilhados, como pools de conexão com bancos de dados, configurações globais ou sistemas de log.

---

## ✅ Exemplo: Database Connection (C#)

```csharp
public sealed class DatabaseConnection {
    private static DatabaseConnection _instance = null;
    private static readonly object _lock = new object();

    // Construtor privado impede instanciação externa
    private DatabaseConnection() {
        Console.WriteLine("Conexão com Banco de Dados aberta.");
    }

    public static DatabaseConnection Instance {
        get {
            // Thread-safe Singleton
            lock (_lock) {
                if (_instance == null) {
                    _instance = new DatabaseConnection();
                }
                return _instance;
            }
        }
    }

    public void Execute(string query) => Console.WriteLine($"Executando: {query}");
}

// Uso:
DatabaseConnection db = DatabaseConnection.Instance;
db.Execute("SELECT * FROM users");
```

## ⚠️ Cuidados
*   **Dificulta testes:** Singleton é uma dependência global oculta. Prefira injeção de dependência se possível.
*   **Concorrência:** Sempre implemente de forma thread-safe (como no exemplo acima usando `lock`).

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[DIP - Dependency Inversion Principle]] (Como evitar singletons acoplados)
