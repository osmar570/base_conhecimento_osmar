# Detalhamento das Camadas: Entities e Use Cases

No centro da [[Clean Architecture]], encontramos as camadas que definem a inteligência do software. Elas devem ser protegidas de qualquer mudança em tecnologias externas (bancos de dados, frameworks, etc.).

---

## 1. Entities (Entidades)

As **Entities** representam as **Regras de Negócio Corporativas**. Elas são os objetos de domínio que contêm dados e comportamentos que seriam verdadeiros mesmo se não existisse um software (ex: um banco sempre precisa validar se um cliente tem saldo antes de um saque).

### Características:
*   **Independência Total:** Não dependem de nada externo.
*   **Estabilidade:** Devem ser a parte do código que menos muda.
*   **Encapsulamento:** Contêm a lógica que garante a integridade dos dados (validações de negócio).

### Exemplo Prático:
```typescript
class Produto {
  constructor(
    public readonly id: string,
    public nome: string,
    public preco: number
  ) {
    if (preco < 0) throw new Error("Preço não pode ser negativo");
  }

  aplicarDesconto(porcentagem: number) {
    this.preco -= (this.preco * porcentagem) / 100;
  }
}
```

---

## 2. Use Cases (Casos de Uso / Interactors)

Os **Use Cases** representam as **Regras de Negócio da Aplicação**. Eles orquestram o fluxo de dados de e para as entidades e utilizam as entidades para atingir os objetivos do caso de uso.

### Características:
*   **Orquestração:** Eles dizem "quem faz o quê". Buscam dados em um repositório, chamam métodos das entidades e salvam o resultado.
*   **Específicos da App:** Contêm lógica que só faz sentido para esta aplicação específica (ex: "Enviar um e-mail após o cadastro").
*   **Dependência:** Dependem apenas das Entidades e de Interfaces (Abstrações).

### Exemplo Prático:
```typescript
class AplicarDescontoNoProduto {
  constructor(private repo: ProdutoRepository) {} // Injeção de Dependência

  async executar(produtoId: string, desconto: number): Promise<void> {
    const produto = await this.repo.buscarPorId(produtoId);
    
    // O Caso de Uso orquestra, mas a regra de desconto está na Entidade
    produto.aplicarDesconto(desconto);
    
    await this.repo.salvar(produto);
  }
}
```

---

## 3. A Diferença Fundamental

| Camada | Escopo | Pergunta que responde |
| :--- | :--- | :--- |
| **Entities** | Negócio (Geral) | "O que é este objeto e quais suas regras básicas?" |
| **Use Cases** | Aplicação (Processo) | "Como eu realizo esta tarefa específica no sistema?" |

---
**Links Relacionados:**
- [[Clean Architecture]] (Visão Geral)
- [[Regra da Dependência e DIP]] (Como as camadas se comunicam)
- [[Interface Adapters (Controllers e Gateways)]]
