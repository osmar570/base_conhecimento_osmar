# Interface Adapters (Controllers, Gateways e Presenters)

A camada de **Interface Adapters** (Adaptadores de Interface) atua como um tradutor. Ela converte dados do formato mais conveniente para as camadas externas (como uma requisição HTTP ou linhas de um banco de dados) para o formato exigido pelas camadas internas ([[Detalhamento das Camadas (Entities e Use Cases)|Casos de Uso e Entidades]]).

---

## 1. O Papel do Adaptador

Nesta camada, o software começa a se conectar com ferramentas específicas, mas ainda de forma protegida. 

*   **Entrada (Input):** O adaptador recebe dados (ex: JSON de uma API) e os transforma em um objeto que o Caso de Uso entende (um DTO - Data Transfer Object).
*   **Saída (Output):** O adaptador recebe a resposta do Caso de Uso e a transforma em um formato para o usuário (ex: um status 201 JSON ou uma página HTML).

---

## 2. Principais Componentes

### A. Controllers (Controladores)
São os responsáveis por receber a entrada do usuário. 
*   **Exemplo:** Um Controller do Express.js que recebe um `req.body`, valida o formato e chama o método `executar()` de um Caso de Uso.

### B. Gateways / Repositories (Portais)
São as implementações das interfaces definidas nos Casos de Uso. 
*   **Exemplo:** A classe `SqlUsuarioRepository` que contém o código SQL real. Ela "conecta" o Caso de Uso ao banco de dados específico, mas o Caso de Uso nunca vê o SQL, apenas chama métodos como `salvar()`.

### C. Presenters (Apresentadores)
Transformam os dados de retorno do Caso de Uso em uma estrutura amigável para a visualização.
*   **Exemplo:** Formatar uma data ou traduzir mensagens de erro antes de enviar para o Frontend.

---

## 3. Exemplo Prático (Tradutor de Dados)

**Controller (Adaptando a Web para o Caso de Uso):**
```typescript
class CriarProdutoController {
  constructor(private useCase: CriarProdutoUseCase) {}

  async handle(httpRequest: any) {
    const { nome, valor } = httpRequest.body;
    
    // Traduz do formato Web para o que o Caso de Uso espera
    const input = { nomeProduto: nome, preco: valor };
    
    try {
      const output = await this.useCase.executar(input);
      return { statusCode: 201, body: output };
    } catch (error) {
      return { statusCode: 400, body: error.message };
    }
  }
}
```

---

## 4. Por que esta camada é importante?

Sem os adaptadores, seu Caso de Uso teria que lidar diretamente com objetos do Express (como `req` e `res`) ou bibliotecas de banco de dados (como `Prisma` ou `TypeORM`). 
Se você decidisse trocar o Express pelo NestJS, teria que reescrever toda a sua lógica de negócio. Com os **Interface Adapters**, você só troca o Controller.

---
**Links Relacionados:**
- [[Clean Architecture]]
- [[Regra da Dependência e DIP]] (Inversão de Dependência)
- [[Detalhamento das Camadas (Entities e Use Cases)]]
