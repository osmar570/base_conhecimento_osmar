# Padrões Criacionais (Creational Patterns)

Os **Padrões Criacionais** lidam com os mecanismos de criação de objetos, buscando criar objetos de uma forma adequada à situação. O objetivo principal é isolar o sistema de como seus objetos são criados, compostos e representados.

## 🧠 Por que eles pertencem a esta classe?

Esses padrões são agrupados aqui porque todos eles resolvem o problema da **instanciação direta** (o uso excessivo do operador `new`). Eles pertencem a esta categoria pois:

1.  **Encapsulam o Conhecimento Concreto:** O sistema não precisa saber qual classe específica está sendo instanciada (ex: `PdfDocument` vs `WordDocument`).
2.  **Ocultam a Complexidade:** Se a criação de um objeto exige muitos passos ou configurações (como no caso do **Builder**), essa complexidade é escondida do cliente.
3.  **Controlam o Ciclo de Vida:** Garantem regras específicas de existência, como no **Singleton**, onde apenas uma instância pode existir.
4.  **Promovem o Desacoplamento:** Ao depender de interfaces ou fábricas, o código torna-se independente das classes concretas, facilitando a manutenção e testes.

## 🛠️ Padrões nesta categoria:
- [[Criacionais/Factory Method|Factory Method]]: Delega a criação para as subclasses.
- [[Criacionais/Abstract Factory|Abstract Factory]]: Cria famílias de objetos relacionados.
- [[Criacionais/Builder|Builder]]: Constrói objetos complexos passo a passo.
- [[Criacionais/Singleton|Singleton]]: Garante instância única global.

---
**Links Relacionados:**
- [[Design Patterns]] (Índice Central)
- [[SOLID]] (Especialmente o Princípio da Inversão de Dependência)
