# ⏱️ Complexidade e Notação Big O

A Notação Big O é a linguagem matemática usada para descrever o desempenho ou a complexidade de um algoritmo. Ela foca em como o tempo de execução ou o uso de memória cresce à medida que o tamanho dos dados de entrada ($n$) aumenta.

---

## 📈 As Complexidades Mais Comuns

### 1. $O(1)$ - Tempo Constante
O desempenho não muda, independentemente do tamanho dos dados.
- **Exemplo:** Acessar um elemento de um Array pelo índice.

### 2. $O(\log n)$ - Tempo Logarítmico
O tempo aumenta de forma muito lenta. Geralmente associado a algoritmos que dividem o problema pela metade a cada passo.
- **Exemplo:** Busca Binária.

### 3. $O(n)$ - Tempo Linear
O tempo cresce proporcionalmente ao número de elementos.
- **Exemplo:** Percorrer um array com um loop simples (`foreach`).

### 4. $O(n \log n)$ - Tempo Linear-Logarítmico
Comum em algoritmos de ordenação eficientes.
- **Exemplo:** Merge Sort, Quick Sort.

### 5. $O(n^2)$ - Tempo Quadrático
O tempo cresce exponencialmente em relação ao tamanho dos dados. Geralmente loops aninhados.
- **Exemplo:** Bubble Sort ou percorrer uma matriz quadrada.

---

## ⚖️ Tempo vs. Espaço (Time vs. Space Complexity)

Ao analisar um algoritmo, olhamos para dois fatores:
1.  **Time Complexity:** Quanto tempo o algoritmo leva para rodar.
2.  **Space Complexity:** Quanta memória extra o algoritmo consome durante a execução.

---

## 🎯 Regras de Ouro para Análise

1.  **Sempre considere o pior caso (Worst Case):** O Big O descreve o limite superior de tempo.
2.  **Remova as constantes:** $O(2n)$ vira $O(n)$.
3.  **Remova os termos não dominantes:** $O(n^2 + n)$ vira $O(n^2)$.
4.  **Loops aninhados multiplicam:** Um loop dentro de outro loop resulta em $O(n \times n) = O(n^2)$.

---

## 📊 Gráfico de Comparação

- **Excelente:** $O(1)$, $O(\log n)$
- **Bom:** $O(n)$
- **Ok:** $O(n \log n)$
- **Ruim:** $O(n^2)$, $O(2^n)$, $O(n!)$

---

## 🔗 Links Internos
- [[Estrutura de Dados]]
- [[01. Fundamentos]]
