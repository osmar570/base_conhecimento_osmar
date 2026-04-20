# Design Patterns (Padrões de Projeto)

Design Patterns são soluções comprovadas para problemas recorrentes no desenvolvimento de software. Eles não são pedaços de código prontos, mas sim **estratégias arquiteturais** para estruturar seu sistema de forma escalável e manutenível.

---

## 🏗️ Padrões Criacionais (Creational)
Focam em abstrair e controlar o processo de criação de objetos.
- [[Factory Method]]: Define uma interface para criar um objeto, deixando as subclasses decidirem.
- [[Abstract Factory]]: Cria famílias de objetos relacionados sem especificar suas classes concretas.
- [[Singleton]]: Garante que uma classe tenha apenas uma instância e fornece acesso global.
- [[Builder]]: Constrói objetos complexos passo a passo com uma interface fluida.

---

## 🏛️ Padrões Estruturais (Structural)
Focam em como classes e objetos são compostos para formar estruturas maiores.
- [[Adapter]]: Permite que interfaces incompatíveis trabalhem juntas.
- [[Decorator]]: Adiciona comportamentos a um objeto dinamicamente (camadas extras).
- [[Proxy]]: Atua como intermediário para controlar o acesso (Lazy Loading, Segurança).
- [[Facade]]: Simplifica o uso de subsistemas complexos em uma única interface.

---

## 🔄 Padrões Comportamentais (Behavioral)
Focam na comunicação e distribuição de responsabilidades entre objetos.
- [[Strategy]]: Torna algoritmos intercambiáveis em tempo de execução.
- [[Observer]]: Notifica múltiplos objetos sobre mudanças de estado (Event-Driven).
- [[State]]: Altera o comportamento de um objeto conforme seu estado interno muda.
- [[Command]]: Encapsula uma solicitação como um objeto (suporta Undo/Redo).

---

## 🚀 Quando Usar Design Patterns?
- **Resolva o problema primeiro:** Não force padrões onde eles não são necessários. Use-os para combater a rigidez, a fragilidade ou a duplicação do código.
- **Conheça o SOLID:** A maioria dos padrões de projeto são aplicações diretas dos princípios SOLID para resolver problemas específicos de flexibilidade.

---
**Links Relacionados:**
- [[SOLID]] (Os princípios por trás dos padrões)
- [[Clean Architecture]] (Padrões usados para estruturar sistemas inteiros)
- [[Engenharia de Software]] (Índice principal)
