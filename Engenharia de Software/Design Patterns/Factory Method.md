# Factory Method (Método de Fábrica)

> "Define uma interface para criar um objeto, mas deixa as subclasses decidirem qual classe instanciar."

O **Factory Method** permite que uma classe adie a instanciação para as subclasses, promovendo o desacoplamento entre o código que utiliza o objeto e o código que o cria.

---

## ❌ Sem Factory Method
Se você precisa criar diferentes tipos de documentos e faz isso diretamente com `new`, o seu código fica acoplado a implementações concretas.

```csharp
public class DocumentEditor {
    public void Open(string type) {
        if (type == "PDF") {
            var pdf = new PdfDocument();
            pdf.Open();
        } else if (type == "Word") {
            var word = new WordDocument();
            word.Open();
        }
    }
}
```

## ✅ Com Factory Method
O editor de documentos não sabe qual documento está criando; ele apenas chama o método de fábrica.

```csharp
public abstract class Document {
    public abstract void Open();
}

public class PdfDocument : Document {
    public override void Open() => Console.WriteLine("Abrindo PDF...");
}

public abstract class DocumentCreator {
    public abstract Document CreateDocument(); // Factory Method
}

public class PdfCreator : DocumentCreator {
    public override Document CreateDocument() => new PdfDocument();
}

// Uso:
DocumentCreator creator = new PdfCreator();
Document doc = creator.CreateDocument();
doc.Open();
```

---
**Links Relacionados:**
- [[Design Patterns]] (Visão Geral)
- [[SOLID]] (Especialmente o DIP)
