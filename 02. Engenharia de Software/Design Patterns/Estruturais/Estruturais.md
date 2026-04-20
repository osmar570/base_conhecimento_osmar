# Padrões Estruturais (Structural Patterns)

Os **Padrões Estruturais** explicam como montar objetos e classes em estruturas maiores, mantendo essas estruturas flexíveis e eficientes. O objetivo principal é garantir que, se uma parte de um sistema mudar, o sistema todo não precise ser reconstruído.

## 🧠 Por que eles pertencem a esta classe?

Esses padrões são agrupados aqui porque todos eles lidam com a **composição** e o **relacionamento entre entidades**. Eles pertencem a esta categoria pois:

1.  **Uniformizam Interfaces Incompatíveis:** No caso do **Adapter**, ele permite que duas classes incompatíveis se comuniquem através de uma nova estrutura.
2.  **Adicionam Camadas de Responsabilidade:** O **Decorator** e o **Proxy** criam estruturas de "envelopamento" (wrappers) que adicionam comportamento sem alterar o objeto original.
3.  **Simplificam Sistemas Complexos:** O **Facade** cria uma estrutura simplificada para uma fachada que esconde toda a complexidade de subsistemas internos.
4.  **Promovem a Extensibilidade:** Ao usar composição em vez de herança (como no **Decorator**), o sistema torna-se muito mais flexível para mudanças futuras.

## 🛠️ Padrões nesta categoria:
- [[Estruturais/Adapter|Adapter]]: Adapta interfaces incompatíveis.
- [[Estruturais/Decorator|Decorator]]: Adiciona responsabilidades dinamicamente.
- [[Estruturais/Proxy|Proxy]]: Controla o acesso ao objeto real.
- [[Estruturais/Facade|Facade]]: Simplifica a interface de subsistemas complexos.

---
**Links Relacionados:**
- [[Design Patterns]] (Índice Central)
- [[Clean Architecture]] (O uso de Adapters é fundamental para o isolamento de camadas)
