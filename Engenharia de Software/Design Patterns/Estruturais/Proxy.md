# Proxy (Procurador)

> "Fornece um substituto ou marcador para outro objeto para controlar o acesso a ele."

O **Proxy** atua como um intermediário. Ele pode ser usado para **Lazy Loading** (carregar um objeto pesado apenas quando necessário), **Segurança** (verificar permissões antes de chamar o objeto real) ou **Logging**.

---

## ✅ Exemplo: Proxy de Acesso a Vídeo (C#)

```csharp
public interface IVideoService {
    void Play(string id);
}

// Objeto real "pesado"
public class VideoService : IVideoService {
    public void Play(string id) => Console.WriteLine($"Rodando vídeo {id}...");
}

// Proxy de Segurança
public class VideoProxy : IVideoService {
    private readonly VideoService _service;
    private readonly string _userRole;

    public VideoProxy(string userRole) {
        _service = new VideoService();
        _userRole = userRole;
    }

    public void Play(string id) {
        if (_userRole == "Admin") {
            _service.Play(id);
        } else {
            Console.WriteLine("Acesso negado: Somente administradores podem ver vídeos.");
        }
    }
}

// Uso:
IVideoService player = new VideoProxy("User");
player.Play("123"); // Negado
```

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[Observabilidade e SRE]] (Proxies são usados para injetar logs e métricas)
