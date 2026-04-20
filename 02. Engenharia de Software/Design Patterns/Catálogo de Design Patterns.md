# 🗃️ Catálogo de Design Patterns

Este catálogo reúne soluções consagradas para problemas recorrentes no design de software orientado a objetos. Os padrões estão divididos em três categorias principais, conforme a classificação original do GoF (Gang of Four).

---

## 🏗️ Padrões Criacionais
*Focam na abstração do processo de instanciação e na criação controlada de objetos.*

| Padrão | Descrição Resumida | Link |
| :--- | :--- | :--- |
| **Factory Method** | Delega a criação de um objeto para as subclasses. | [[Criacionais/Factory Method\|Ver Detalhes]] |
| **Abstract Factory** | Cria famílias de objetos relacionados sem especificar classes concretas. | [[Criacionais/Abstract Factory\|Ver Detalhes]] |
| **Singleton** | Garante que uma classe tenha apenas uma instância global. | [[Criacionais/Singleton\|Ver Detalhes]] |
| **Builder** | Separa a construção de um objeto complexo da sua representação. | [[Criacionais/Builder\|Ver Detalhes]] |

> [!INFO] Saiba mais: [[Criacionais/Criacionais\|O que são Padrões Criacionais?]]

---

## 🏛️ Padrões Estruturais
*Lidam com a composição de classes e objetos para formar estruturas maiores e flexíveis.*

| Padrão | Descrição Resumida | Link |
| :--- | :--- | :--- |
| **Adapter** | Converte uma interface incompatível em uma interface esperada. | [[Estruturais/Adapter\|Ver Detalhes]] |
| **Decorator** | Adiciona responsabilidades a um objeto dinamicamente (Wrappers). | [[Estruturais/Decorator\|Ver Detalhes]] |
| **Proxy** | Fornece um substituto para controlar o acesso a um objeto real. | [[Estruturais/Proxy\|Ver Detalhes]] |
| **Facade** | Fornece uma interface simplificada para um sistema complexo. | [[Estruturais/Facade\|Ver Detalhes]] |

> [!INFO] Saiba mais: [[Estruturais/Estruturais\|O que são Padrões Estruturais?]]

---

## 🔄 Padrões Comportamentais
*Concentram-se nos algoritmos e na distribuição de responsabilidades entre objetos.*

| Padrão | Descrição Resumida | Link |
| :--- | :--- | :--- |
| **Strategy** | Torna algoritmos intercambiáveis em tempo de execução. | [[Comportamentais/Strategy\|Ver Detalhes]] |
| **Observer** | Define uma dependência um-para-muitos (Event-Driven). | [[Comportamentais/Observer\|Ver Detalhes]] |
| **State** | Permite que um objeto mude de comportamento ao mudar de estado. | [[Comportamentais/State\|Ver Detalhes]] |
| **Command** | Encapsula uma solicitação como um objeto, permitindo filas e undo. | [[Comportamentais/Command\|Ver Detalhes]] |

> [!INFO] Saiba mais: [[Comportamentais/Comportamentais\|O que são Padrões Comportamentais?]]

---

## 🚀 Como Escolher um Padrão?

1. **Analise o Problema:** O problema é de criação, estruturação ou comportamento?
2. **Avalie os Trade-offs:** Todo padrão adiciona uma camada de complexidade/abstração. Vale a pena o custo?
3. **Siga o SOLID:** Os padrões são ferramentas para atingir os princípios [[../SOLID/SOLID\|SOLID]]. Se o seu código viola o SOLID, um padrão pode ser a solução.

---
**Links Relacionados:**
- [[../02. Engenharia de Software\|Engenharia de Software]]
- [[../Clean Architecture/Clean Architecture\|Clean Architecture]]
