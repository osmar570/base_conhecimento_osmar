# 🔢 Arrays (Vetores)

Arrays são a estrutura de dados mais fundamental e amplamente utilizada. Eles armazenam uma coleção de elementos do mesmo tipo em locais de memória **contíguos** (vizinhos).

---

## 🧠 Conceitos Fundamentais

### 1. Acesso por Índice
A principal característica do Array é o acesso direto. Como os dados estão em sequência, o computador calcula o endereço de memória exato de qualquer elemento usando uma fórmula simples:
`Endereço = Início + (Índice * Tamanho_do_Tipo)`
Isso torna o acesso extremamente rápido.

### 2. Tamanho Fixo vs. Dinâmico
- **Estáticos:** O tamanho é definido na compilação e não muda (ex: C, Java arrays puros).
- **Dinâmicos:** Redimensionam-se automaticamente conforme necessário (ex: `List<T>` em C#, `ArrayList` em Java, `std::vector` em C++).

---

## ⏱️ Complexidade (Big O)

| Operação | Complexidade | Explicação |
| :--- | :--- | :--- |
| **Acesso (Lookup)** | $O(1)$ | Acesso imediato via índice. |
| **Busca (Search)** | $O(n)$ | É necessário percorrer o array no pior caso. |
| **Inserção** | $O(n)$ | Requer deslocar todos os elementos seguintes. |
| **Remoção** | $O(n)$ | Requer deslocar os elementos para preencher o buraco. |

> **Nota:** Inserir no final de um array dinâmico é, em média (amortizado), $O(1)$.

---

## ✅ Vantagens e ❌ Desvantagens

### Vantagens
- **Velocidade de Acesso:** Imbatível para leitura quando se sabe o índice.
- **Eficiência de Cache:** Devido à contiguidade na memória, aproveitam muito bem o cache do processador (Spatial Locality).

### Desvantagens
- **Custo de Inserção/Remoção:** Caro se feito no início ou meio da lista.
- **Desperdício de Memória:** Arrays dinâmicos costumam alocar mais espaço do que o necessário para evitar realocações frequentes.

---

## 💻 Exemplos em C#

### 1. Array Estático (Tamanho Fixo)
```csharp
// Declaração e inicialização
int[] numeros = new int[5] { 10, 20, 30, 40, 50 };

// Acesso O(1)
int terceiroElemento = numeros[2]; // 30

// Alteração O(1)
numeros[0] = 100;

// Percorrendo o array O(n)
foreach (var n in numeros)
{
    Console.WriteLine(n);
}
```


### 2. Array Dinâmico
Em C#, a classe `List<T>` encapsula um array que cresce automaticamente conforme necessário.

```csharp
using System.Collections.Generic;

List<string> nomes = new List<string>();

//adição no final : 0(1) amortizado
nomes.Add("Osmar");
nomes.Add("Gemini");

//Inserção no meio: 0(n) - requer deslocar elementos
nomes.Insert(1, "Sênior");

//Remoção: 0(n) - requer preencher o espaço
nomes.RemoveAt(0);

//Busca por valor: 0(n)
bool existe = nomes.Contains("Gemini");

```

--- 
## 🔗 Links Internos
- [[Estrutura de Dados]]
- [[01. Fundamentos]]