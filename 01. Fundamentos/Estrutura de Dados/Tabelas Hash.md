# 🔑 Tabelas Hash (Hash Tables)

Uma Tabela Hash (ou Mapa Hash) é uma estrutura de dados que mapeia **chaves** para **valores**. Ela utiliza uma **Função Hash** para calcular um índice em um array, onde o valor correspondente pode ser encontrado.

---

## 🧠 Como Funciona

### 1. Chave e Valor
- **Chave (Key):** Um identificador único (ex: CPF, ID de usuário, nome de arquivo).
- **Valor (Value):** O dado associado àquela chave.

### 2. Função Hash (Hash Function)
É o "cérebro" da estrutura. Ela recebe uma chave e retorna um número inteiro (índice). Uma boa função hash deve:
- Ser rápida de calcular.
- Distribuir as chaves uniformemente para evitar colisões.
- Ser determinística (mesma entrada sempre gera a mesma saída).

---

## 💥 Colisões

Uma colisão ocorre quando duas chaves diferentes resultam no mesmo índice após passarem pela função hash. Existem duas formas principais de resolver isso:

1.  **Encadeamento Separado (Chaining):** Cada posição do array armazena uma **[[Listas Ligadas|Lista Ligada]]**. Se houver colisão, o novo item é adicionado à lista.
2.  **Endereçamento Aberto (Open Addressing):** Se houver colisão, a tabela procura o próximo espaço vazio disponível no array (Linear Probing, Quadratic Probing).

---

## ⏱️ Complexidade (Big O)

| Operação | Caso Médio | Pior Caso (Muitas Colisões) |
| :--- | :--- | :--- |
| **Busca** | $O(1)$ | $O(n)$ |
| **Inserção** | $O(1)$ | $O(n)$ |
| **Remoção** | $O(1)$ | $O(n)$ |

> **Nota:** Na prática, as Tabelas Hash são extremamente eficientes e operam quase sempre em tempo constante.

---

## 🧠 Casos de Uso Reais

1.  **Bancos de Dados:** Indexação para busca rápida.
2.  **Caches:** Armazenamento temporário de dados (ex: Redis).
3.  **Compiladores:** Tabelas de símbolos para armazenar variáveis e funções.
4.  **Dicionários e Sets:** Implementação nativa em linguagens (ex: `Dictionary` em C#, `dict` em Python, `Map` em JS).

---

## 💻 Exemplos em C#

No ecossistema .NET, a implementação mais comum e recomendada de uma Tabela Hash é a classe genérica `Dictionary<TKey, TValue>`.

### 1. Usando Dictionary<TKey, TValue>
```csharp
using System;
using System.Collections.Generic;

// Inicialização (Chave: int, Valor: string)
Dictionary<int, string> alunos = new Dictionary<int, string>();

// Inserção O(1)
alunos.Add(101, "Osmar");
alunos.Add(102, "Ana");
alunos[103] = "Carlos"; // Outra forma de inserir/atualizar

// Acesso/Busca O(1)
if (alunos.TryGetValue(101, out string nome))
{
    Console.WriteLine($"Aluno encontrado: {nome}");
}

// Remoção O(1)
alunos.Remove(102);

// Verificando existência O(1)
bool existe = alunos.ContainsKey(103);
```

### 2. O Método GetHashCode()
Em C#, todos os objetos herdam o método `GetHashCode()` da classe `Object`. Este método é a base da **Função Hash** usada internamente pelo Dictionary.

```csharp
string texto = "Gemini";
int hash = texto.GetHashCode();
Console.WriteLine($"O Hash de '{texto}' é: {hash}");
```

---

## 🔗 Links Internos
- [[Estrutura de Dados]]
- [[Arrays]]
- [[Listas Ligadas]]
