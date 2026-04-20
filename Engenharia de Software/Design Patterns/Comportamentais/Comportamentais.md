# Padrões Comportamentais (Behavioral Patterns)

Os **Padrões Comportamentais** tratam dos algoritmos e da atribuição de responsabilidades entre os objetos. Eles não descrevem apenas padrões de objetos ou classes, mas também os padrões de comunicação entre eles.

## 🧠 Por que eles pertencem a esta classe?

Esses padrões são agrupados aqui porque todos eles lidam com a **dinâmica da comunicação e o comportamento** do sistema em tempo de execução. Eles pertencem a esta categoria pois:

1.  **Encapsulam o Algoritmo:** O **Strategy** permite que o comportamento do sistema mude independentemente do seu uso, encapsulando lógicas complexas.
2.  **Gerenciam Transições de Estado:** O **State** permite que um objeto se comporte de formas totalmente diferentes conforme seu estado interno muda, sem exigir longas cadeias de `if/else`.
3.  **Desacoplam a Solicitação da Execução:** O **Command** encapsula o que deve ser feito em um objeto, permitindo agendar, desfazer ou enfileirar ações.
4.  **Promovem a Notificação e Reação:** O **Observer** cria um canal de comunicação de um-para-muitos, permitindo que vários objetos reajam a eventos de forma automática e desacoplada.

## 🛠️ Padrões nesta categoria:
- [[Comportamentais/Strategy|Strategy]]: Define lógicas de algoritmos intercambiáveis.
- [[Comportamentais/Observer|Observer]]: Notifica múltiplos dependentes sobre mudanças.
- [[Comportamentais/State|State]]: Muda o comportamento conforme o estado interno.
- [[Comportamentais/Command|Command]]: Encapsula pedidos como objetos.

---
**Links Relacionados:**
- [[Design Patterns]] (Índice Central)
- [[Observabilidade e SRE]] (O padrão Observer é a base para o monitoramento reativo)
