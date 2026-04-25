# 🔗 Listas Ligadas (Linked Lists)

Uma Lista Ligada é uma estrutura de dados linear onde os elementos não são armazenados em locais de memória contíguos. Em vez disso, cada elemento (chamado de **Nó**) contém os dados e uma referência (ponteiro) para o próximo nó da sequência.

---

## 🧠 Estrutura de um Nó
Um nó básico é composto por:
1. **Dado:** O valor armazenado.
2. **Next (Próximo):** Um ponteiro/referência para o próximo nó.

---

## 🏗️ Tipos de Listas Ligadas

### 1. Simplesmente Ligada (Singly Linked List)
Cada nó aponta apenas para o próximo. A navegação é unidirecional.

### 2. Duplamente Ligada (Doubly Linked List)
Cada nó possui dois ponteiros: um para o **próximo** e outro para o **anterior**. Permite navegação em ambos os sentidos, facilitando remoções.

### 3. Circular
O último nó aponta de volta para o primeiro (Head), formando um ciclo.

---

## ⏱️ Complexidade (Big O)

| Operação | Complexidade | Explicação |
| :--- | :--- | :--- |
| **Acesso (Lookup)** | $O(n)$ | É necessário percorrer a lista do início até o índice desejado. |
| **Busca (Search)** | $O(n)$ | Pior caso: percorrer toda a lista. |
| **Inserção (Início)**| $O(1)$ | Basta atualizar os ponteiros do novo nó e da "Head". |
| **Inserção (Meio)**  | $O(n)$ | Requer buscar a posição primeiro ($O(n)$). |
| **Remoção (Início)** | $O(1)$ | Operação imediata. |

---

## ⚖️ Arrays vs. Listas Ligadas

| Característica | Arrays | Listas Ligadas |
| :--- | :--- | :--- |
| **Tamanho** | Fixo (ou redimensionamento caro) | Dinâmico e flexível |
| **Acesso** | Rápido $O(1)$ | Lento $O(n)$ |
| **Memória** | Melhor aproveitamento (contíguo) | Mais overhead (guarda ponteiros) |
| **Inserção/Remoção** | Cara (requer shift de elementos) | Barata (basta mudar ponteiros) |

---

## 💻 Exemplos em C#

### 1. Usando a classe nativa
O .NET fornece uma implementação de **Lista Duplamente Ligada**.

```csharp
using System.Collections.Generic;

LinkedList<string> lista = new LinkedList<string>();

// Adição O(1)
lista.AddFirst("Primeiro");
lista.AddLast("Último");

// Adição após um nó específico O(1)
LinkedListNode<string> node = lista.Find("Primeiro");
lista.AddAfter(node, "Segundo");

// Remoção O(1) se você tiver a referência do nó
lista.RemoveFirst();

// Percorrendo a lista O(n)
foreach (var item in lista)
{
    Console.WriteLine(item);
}
```

### 2. Implementação Conceitual (Singly Linked List)
Como seria a estrutura básica de um nó personalizado:
```csharp
public class Node
{
    public int Data { get; set; }
    public Node Next { get; set; }

    public Node(int data)
    {
        Data = data;
        Next = null;
    }
}

// Exemplo de uso:
Node head = new Node(1);
head.Next = new Node(2);
head.Next.Next = new Node(3);
```

---

## 🔗 Links Internos
- [[Arrays]]
- [[Estrutura de Dados]]
- [[01. Fundamentos]]
