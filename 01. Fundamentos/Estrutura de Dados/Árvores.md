# 🌳 Árvores (Trees)

Uma Árvore é uma estrutura de dados **não-linear** e **hierárquica**, composta por nós conectados por arestas. Ao contrário de arrays ou listas ligadas, as árvores organizam os dados de forma descendente.

---

## 🧠 Terminologia Básica

- **Raiz (Root):** O nó no topo da árvore (o único que não tem pai).
- **Nó (Node):** Uma entidade que contém um valor e ponteiros para outros nós.
- **Aresta (Edge):** A conexão entre dois nós.
- **Pai e Filho (Parent/Child):** Um nó é pai de qualquer nó conectado diretamente abaixo dele.
- **Folha (Leaf):** Um nó que não possui filhos (fim de um ramo).
- **Subárvore:** Uma árvore formada por um nó e todos os seus descendentes.
- **Altura (Height):** O número de arestas no caminho mais longo da raiz até uma folha.

---

## 🏗️ Tipos Comuns de Árvores

### 1. Árvore Binária (Binary Tree)
Cada nó pode ter no máximo **dois filhos**, referenciados como filho esquerdo e filho direito.

### 2. Árvore Binária de Busca (BST - Binary Search Tree)
Uma árvore binária com a propriedade de ordenação:
- Valores na subárvore **esquerda** são menores que o pai.
- Valores na subárvore **direita** são maiores que o pai.
- Permite buscas eficientes.

### 3. Árvores Balanceadas (AVL e Red-Black)
Árvores que se auto-ajustam para manter a altura mínima, garantindo que as operações de busca permaneçam rápidas mesmo com muitas inserções.

### 4. Heap
Uma árvore binária especial usada para implementar Filas de Prioridade.
- **Max-Heap:** O pai é sempre maior ou igual aos filhos.
- **Min-Heap:** O pai é sempre menor ou igual aos filhos.

---

## ⏱️ Complexidade em Árvores Binárias de Busca (BST)

| Operação | Caso Médio (Balanceada) | Pior Caso (Desbalanceada) |
| :--- | :--- | :--- |
| **Busca** | $O(\log n)$ | $O(n)$ |
| **Inserção** | $O(\log n)$ | $O(n)$ |
| **Remoção** | $O(\log n)$ | $O(n)$ |

> **Nota:** Se uma BST se tornar uma linha reta (desbalanceada), ela se comporta como uma Lista Ligada.

---

## 🔍 Percursos (Traversals)

Como visitar todos os nós de uma árvore:
1.  **In-Order (In-fixo):** Esquerda -> Raiz -> Direita (retorna os valores ordenados em uma BST).
2.  **Pre-Order (Pré-fixo):** Raiz -> Esquerda -> Direita.
3.  **Post-Order (Pós-fixo):** Esquerda -> Direita -> Raiz.
4.  **Level-Order (Nível):** Visita os nós nível por nível (usando uma Fila).

---

## 🧠 Casos de Uso Reais

1.  **Sistemas de Arquivos:** Pastas e subpastas em sistemas operacionais.
2.  **DOM (Document Object Model):** Representação de páginas HTML nos browsers.
3.  **Bancos de Dados:** Utilizam B-Trees e B+Trees para indexação.
4.  **Compiladores:** Árvores de Sintaxe Abstrata (AST) para validar código.

---

## 💻 Exemplos em C#

### 1. Implementação de um Nó de Árvore Binária
Diferente de pilhas e filas, o .NET não possui uma classe `Tree<T>` genérica, pois as árvores variam muito em estrutura. Implementamos a base manualmente:

```csharp
public class TreeNode
{
    public int Value { get; set; }
    public TreeNode Left { get; set; }
    public TreeNode Right { get; set; }

    public TreeNode(int value)
    {
        Value = value;
        Left = null;
        Right = null;
    }
}

// Uso manual:
TreeNode root = new TreeNode(10);
root.Left = new TreeNode(5);
root.Right = new TreeNode(15);
```

### 2. Coleções do .NET que usam Árvores
O .NET utiliza **Árvores Red-Black** (balanceadas) internamente em algumas coleções:

```csharp
using System.Collections.Generic;

// SortedSet mantém os elementos sempre ordenados e balanceados
SortedSet<int> numeros = new SortedSet<int>();
numeros.Add(10);
numeros.Add(5);
numeros.Add(20);

// SortedDictionary mantém as chaves ordenadas usando uma árvore
SortedDictionary<int, string> usuarios = new SortedDictionary<int, string>();
```

---

## 🔗 Links Internos
- [[Estrutura de Dados]]
- [[Filas]] (usadas no percurso Level-Order)
