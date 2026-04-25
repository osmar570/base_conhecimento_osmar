# 📚 Pilhas (Stacks)

Uma Pilha é uma estrutura de dados linear que segue o princípio **LIFO** (*Last-In, First-Out*), ou seja, o último elemento a entrar é o primeiro a sair. 

Imagine uma pilha de pratos: você sempre coloca um novo prato no topo e sempre retira o prato que está no topo.

---

## 🛠️ Operações Principais

| Operação | Descrição | Complexidade |
| :--- | :--- | :--- |
| **Push** | Adiciona um elemento ao topo da pilha. | $O(1)$ |
| **Pop** | Remove e retorna o elemento do topo da pilha. | $O(1)$ |
| **Peek / Top** | Retorna o elemento do topo sem removê-lo. | $O(1)$ |
| **IsEmpty** | Verifica se a pilha está vazia. | $O(1)$ |

---

## 🧠 Casos de Uso Reais

1.  **Gerenciamento de Memória (Stack Trace):** Onde as chamadas de funções de um programa são armazenadas.
2.  **Mecanismos de Undo/Redo (Desfazer/Refazer):** Editores de texto armazenam as ações em uma pilha.
3.  **Navegação no Browser:** O botão "Voltar" utiliza uma pilha de URLs visitadas.
4.  **Avaliação de Expressões Matemáticas:** Conversão de infixa para posfixa e resolução de parênteses.

---

## 🏗️ Implementação

As pilhas podem ser implementadas de duas formas principais:
- **Baseada em Arrays:** Rápida, mas com tamanho fixo (ou custo de redimensionamento).
- **Baseada em Listas Ligadas:** Tamanho dinâmico e inserção/remoção constante, mas com overhead de memória para ponteiros.

---

## 💻 Exemplos em C#

O .NET fornece a classe genérica `Stack<T>` para trabalhar com pilhas de forma eficiente.

```csharp
using System;
using System.Collections.Generic;

// Inicialização
Stack<string> historicoNavegacao = new Stack<string>();

// Push: Adicionando elementos ao topo O(1)
historicoNavegacao.Push("google.com");
historicoNavegacao.Push("github.com");
historicoNavegacao.Push("stackoverflow.com");

// Peek: Apenas observa o topo sem remover O(1)
Console.WriteLine($"No topo agora: {historicoNavegacao.Peek()}"); // stackoverflow.com

// Pop: Remove e retorna o topo O(1)
string paginaAtual = historicoNavegacao.Pop();
Console.WriteLine($"Voltando de: {paginaAtual}"); // Voltando de: stackoverflow.com

// Verificando o estado da pilha
if (historicoNavegacao.Count > 0)
{
    Console.WriteLine($"Próxima página na pilha: {historicoNavegacao.Peek()}");
}

// Limpando a pilha
historicoNavegacao.Clear();
```

---

## 🔗 Links Internos
- [[Arrays]]
- [[Listas Ligadas]]
- [[Estrutura de Dados]]
