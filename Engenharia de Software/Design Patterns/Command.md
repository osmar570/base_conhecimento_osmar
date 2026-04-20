# Command (Comando)

> "Encapsula uma solicitação como um objeto, permitindo parametrizar clientes com diferentes solicitações e suportar operações reversíveis."

O **Command** separa quem envia a solicitação de quem a executa. Ele é muito útil para sistemas que precisam de **Undo/Redo** (Desfazer/Refazer) ou de uma fila de comandos para execução posterior.

---

## ✅ Exemplo: Controle Remoto (C#)

```csharp
public interface ICommand {
    void Execute();
}

// Receptor (Receiver) - Quem sabe fazer a ação
public class Light {
    public void On() => Console.WriteLine("Luz Ligada");
    public void Off() => Console.WriteLine("Luz Desligada");
}

// Comandos Concretos
public class LightOnCommand : ICommand {
    private Light _light;
    public LightOnCommand(Light light) => _light = light;
    public void Execute() => _light.On();
}

// Invocador (Invoker)
public class RemoteControl {
    private ICommand _command;
    public void SetCommand(ICommand c) => _command = c;
    public void PressButton() => _command.Execute();
}

// Uso:
Light myLight = new Light();
RemoteControl remote = new RemoteControl();
remote.SetCommand(new LightOnCommand(myLight));
remote.PressButton();
```

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[Engenharia de Software]] (Comandos são fundamentais em arquiteturas de sistemas distribuídos)
