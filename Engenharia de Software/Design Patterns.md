# Design Patterns (Padrões de Projeto)

Design Patterns são soluções comprovadas para problemas recorrentes no desenvolvimento de software. Eles não são pedaços de código prontos, mas sim **estratégias arquiteturais** para estruturar seu sistema de forma escalável e manutenível.

---

## 🏗️ Categorias de Padrões (GoF - Gang of Four)

### 1. Criacionais (Creational)
Focam em abstrair e controlar o processo de criação de objetos.
- **Factory Method:** Define uma interface para criar um objeto, deixando as subclasses decidirem a classe concreta. Útil para desacoplar a lógica de negócio da infraestrutura.
- **Abstract Factory:** Permite criar famílias de objetos relacionados sem especificar suas classes concretas.
- **Singleton:** Garante que uma classe tenha apenas uma instância e fornece um ponto de acesso global. *Use com cautela para não criar dependências ocultas.*
- **Builder:** Permite construir objetos complexos passo a passo, separando a construção da representação final.

### 2. Estruturais (Structural)
Focam em como classes e objetos são compostos para formar estruturas maiores.
- **Adapter (Adaptador):** Permite que interfaces incompatíveis trabalhem juntas. É a base da **Arquitetura Hexagonal** (Ports and Adapters).
- **Decorator:** Adiciona comportamentos a um objeto dinamicamente (ex: adicionar Logging ou Cache a um serviço sem alterar seu código original).
- **Proxy:** Fornece um substituto ou marcador para outro objeto para controlar o acesso (muito usado em segurança e Lazy Loading).
- **Facade (Fachada):** Fornece uma interface simplificada para um conjunto complexo de classes em um subsistema.

### 3. Comportamentais (Behavioral)
Focam na comunicação e distribuição de responsabilidades entre objetos.
- **Strategy:** Define uma família de algoritmos, encapsula cada um e os torna intercambiáveis. Permite mudar o comportamento em tempo de execução.
- **Observer (Observador):** Define uma dependência um-para-muitos, notificando mudanças de estado. Essencial para sistemas **Event-Driven**.
- **State:** Permite que um objeto altere seu comportamento quando seu estado interno muda.
- **Command:** Encapsula uma solicitação como um objeto, permitindo parametrizar clientes com diferentes solicitações e suportar operações reversíveis (Undo/Redo).

---

## 🚀 Quando Usar Design Patterns?

- **Não force padrões:** Aplicar padrões prematuramente gera "Overengineering" (complexidade desnecessária).
- **Resolva o problema primeiro:** Identifique o ponto de dor (duplicação, rigidez, fragilidade) e então aplique o padrão que resolve aquela dor específica.
- **Conheça o SOLID:** A maioria dos padrões de projeto são aplicações diretas dos princípios SOLID para resolver problemas específicos de flexibilidade.

---
**Links Relacionados:**
- [[SOLID]] (Os princípios por trás dos padrões)
- [[Clean Architecture]] (Padrões usados para estruturar sistemas inteiros)
- [[Engenharia de Software]] (Índice principal)
