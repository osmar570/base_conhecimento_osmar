# 🚶‍♂️ Filas (Queues)

Uma Fila é uma estrutura de dados linear que segue o princípio **FIFO** (*First-In, First-Out*), ou seja, o primeiro elemento a entrar é obrigatoriamente o primeiro a sair. 

Imagine uma fila de banco: a primeira pessoa que chega é a primeira a ser atendida.

---

## 🛠️ Operações Principais

| Operação | Descrição | Complexidade |
| :--- | :--- | :--- |
| **Enqueue** | Adiciona um elemento ao final da fila (Rear/Tail). | $O(1)$ |
| **Dequeue** | Remove e retorna o elemento do início da fila (Front/Head). | $O(1)$ |
| **Peek / Front**| Retorna o elemento do início sem removê-lo. | $O(1)$ |
| **IsEmpty** | Verifica se a fila está vazia. | $O(1)$ |

---

## 🏗️ Variações de Filas

### 1. Fila Circular
O último elemento aponta de volta para o primeiro, otimizando o uso de espaço em implementações baseadas em Arrays (evita o "shift" de elementos).

### 2. Fila de Prioridade (Priority Queue)
Cada elemento possui uma prioridade. Elementos com maior prioridade são removidos antes, independente da ordem de chegada.

### 3. Deque (Double-Ended Queue)
Permite inserção e remoção em ambas as extremidades (início e fim).

---

## 🧠 Casos de Uso Reais

1.  **Escalonamento de Processos (SO):** Processos aguardando tempo de CPU.
2.  **Sistemas de Mensageria:** Filas de tarefas (ex: RabbitMQ, SQS) onde as mensagens são processadas na ordem de chegada.
3.  **Buffer de IO:** Streaming de vídeo ou áudio, buffers de teclado.
4.  **Algoritmos de Busca em Largura (BFS):** Utilizado em grafos e árvores.

---

## 💻 Exemplos em C#

O .NET fornece a classe genérica `Queue<T>` para gerenciar filas de forma eficiente.

```csharp
using System;
using System.Collections.Generic;

// Inicialização
Queue<string> filaDeImpressao = new Queue<string>();

// Enqueue: Adicionando ao final da fila O(1)
filaDeImpressao.Enqueue("Documento_PDF_1");
filaDeImpressao.Enqueue("Relatorio_Financeiro");
filaDeImpressao.Enqueue("Foto_Viagem");

// Peek: Observa o próximo da fila (início) sem remover O(1)
Console.WriteLine($"Próximo para imprimir: {filaDeImpressao.Peek()}"); // Documento_PDF_1

// Dequeue: Remove e retorna o primeiro da fila O(1)
string documentoProcessado = filaDeImpressao.Dequeue();
Console.WriteLine($"Imprimindo agora: {documentoProcessado}");

// Verificando se a fila contém elementos
if (filaDeImpressao.Count > 0)
{
    Console.WriteLine($"Ainda restam {filaDeImpressao.Count} arquivos na fila.");
}
```

---

## 🔗 Links Internos
- [[Pilhas]]
- [[Listas Ligadas]]
- [[Estrutura de Dados]]
