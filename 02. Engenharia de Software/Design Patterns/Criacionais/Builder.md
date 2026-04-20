# Builder (Construtor)

> "Permite a construção de objetos complexos passo a passo, separando a construção da representação final."

O **Builder** evita o problema do "Construtor Telescópico" (quando uma classe tem dezenas de parâmetros opcionais no construtor) e torna o código mais legível e fluido.

---

## ✅ Exemplo: Configuração de Servidor (C#)

```csharp
public class Server {
    public string Host { get; set; }
    public int Port { get; set; }
    public bool UseSsl { get; set; }
    public int MaxConnections { get; set; }
}

public class ServerBuilder {
    private Server _server = new Server();

    public ServerBuilder SetHost(string host) {
        _server.Host = host;
        return this; // Permite Fluent Interface
    }

    public ServerBuilder OnPort(int port) {
        _server.Port = port;
        return this;
    }

    public ServerBuilder WithSsl() {
        _server.UseSsl = true;
        return this;
    }

    public Server Build() => _server;
}

// Uso Fluido:
Server srv = new ServerBuilder()
                .SetHost("localhost")
                .OnPort(8080)
                .WithSsl()
                .Build();
```

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[SRP - Single Responsibility Principle]] (Separa a lógica do objeto da sua construção)
