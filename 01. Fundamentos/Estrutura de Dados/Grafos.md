# 🕸️ Grafos (Graphs)

Um Grafo é uma estrutura de dados não-linear que consiste em um conjunto de nós (chamados de **Vértices**) e as conexões entre eles (chamadas de **Arestas**). É a estrutura mais flexível, capaz de representar quase qualquer tipo de relacionamento.

---

## 🧠 Conceitos Fundamentais

### 1. Componentes
- **Vértice (Vertex/Node):** Um ponto de dados.
- **Aresta (Edge):** Uma linha que conecta dois vértices.

### 2. Tipos de Grafos
- **Dirigido (Directed):** As arestas têm um sentido (setas). A relação de A para B não implica relação de B para A.
- **Não-Dirigido (Undirected):** As arestas não têm direção. A conexão é mútua.
- **Ponderado (Weighted):** As arestas possuem um "peso" ou custo (ex: distância entre cidades).
- **Cíclico vs. Acíclico:** Grafos que contêm ou não caminhos que retornam ao ponto de origem.
    - **DAG (Directed Acyclic Graph):** Muito usado em processamento de dados e Git.

---

## 🏗️ Representação na Memória

Existem duas formas principais de implementar um grafo:

### 1. Matriz de Adjacência
Uma tabela $V \times V$ onde o valor na célula $(i, j)$ indica se há conexão entre o vértice $i$ e $j$.
- **Vantagem:** Consulta de conexão rápida $O(1)$.
- **Desvantagem:** Consome muita memória $O(V^2)$, mesmo para poucas conexões.

### 2. Lista de Adjacência
Cada vértice mantém uma lista de outros vértices aos quais está conectado.
- **Vantagem:** Uso eficiente de memória $O(V + E)$.
- **Desvantagem:** Consulta de conexão mais lenta $O(V)$.

---

## ⏱️ Algoritmos de Busca

1.  **BFS (Breadth-First Search - Busca em Largura):**
    - Explora nível por nível.
    - Usa uma **[[Filas|Fila]]**.
    - Ideal para encontrar o **caminho mais curto** em grafos não ponderados.

2.  **DFS (Depth-First Search - Busca em Profundidade):**
    - Explora o máximo possível ao longo de cada ramo antes de retroceder.
    - Usa uma **[[Pilhas|Pilha]]** (ou recursão).
    - Ideal para detectar ciclos e ordenação topológica.

---

## 🧠 Casos de Uso Reais

1.  **Redes Sociais:** Pessoas são vértices e amizades são arestas.
2.  **Google Maps / GPS:** Interseções são vértices e ruas são arestas ponderadas (distância/tempo).
3.  **Motores de Busca (PageRank):** Páginas web e seus links.
4.  **Redes de Computadores:** Roteadores e cabos de conexão.

---

## 💻 Exemplos em C#

### 1. Implementação de Lista de Adjacência
A forma mais comum de representar grafos em C# é usando um `Dictionary` onde a chave é o vértice e o valor é uma lista de seus vizinhos.

```csharp
using System;
using System.Collections.Generic;

public class Grafo
{
    // Dicionário de Listas de Adjacência
    private Dictionary<string, List<string>> adjacencias = new Dictionary<string, List<string>>();

    public void AdicionarVertice(string v)
    {
        if (!adjacencias.ContainsKey(v))
            adjacencias[v] = new List<string>();
    }

    public void AdicionarAresta(string origem, string destino)
    {
        // Para grafo não-dirigido, adicionamos em ambos os sentidos
        adjacencias[origem].Add(destino);
        adjacencias[destino].Add(origem);
    }

    public void MostrarGrafo()
    {
        foreach (var vertice in adjacencias)
        {
            Console.WriteLine($"{vertice.Key} -> {string.Join(", ", vertice.Value)}");
        }
    }
}

// Uso:
var redesSociais = new Grafo();
redesSociais.AdicionarVertice("Osmar");
redesSociais.AdicionarVertice("Ana");
redesSociais.AdicionarVertice("Carlos");

redesSociais.AdicionarAresta("Osmar", "Ana");
redesSociais.AdicionarAresta("Ana", "Carlos");

redesSociais.MostrarGrafo();
```

---

## 🔗 Links Internos
- [[Estrutura de Dados]]
- [[Filas]]
- [[Pilhas]]
