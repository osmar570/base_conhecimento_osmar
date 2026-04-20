# A Regra da Dependência e Inversão de Dependência (DIP)

Na **Clean Architecture**, a estrutura de pastas e a organização do código são ditadas por uma regra fundamental: as dependências de código devem apontar apenas para dentro, em direção ao núcleo (Regras de Negócio).

## 1. A Regra da Dependência

Imagine o sistema como uma cebola com várias camadas. 
*   **O Núcleo (Entidades e Casos de Uso):** Contém o que sua empresa faz (ex: calcular juros, validar CPF).
*   **O Exterior (Banco de dados, APIs, UI):** Contém as ferramentas que você usa.

**A Regra diz:** Nada nas camadas internas pode saber qualquer coisa sobre algo nas camadas externas. O Caso de Uso não pode importar um `Controller` ou saber que o banco é o `MongoDB`.

## 2. Inversão de Dependência (Dependency Inversion Principle - DIP)

Se o meu **Caso de Uso** (Camada Interna) precisa salvar um dado no **Banco de Dados** (Camada Externa), como ele faz isso sem "conhecer" o banco? 

**A solução é a Inversão de Dependência:**

1.  O Caso de Uso define uma **Interface** (ou Contrato) que diz: *"Eu preciso de algo que consiga salvar um Usuário"*.
2.  Essa Interface fica **dentro** da camada interna.
3.  A camada externa (Banco de Dados) **implementa** essa interface.

### Exemplo Prático (Código Conceitual)

**Camada Interna (Caso de Uso):**
```typescript
// O Caso de Uso não sabe que o banco existe, ele conhece apenas o contrato.
interface UsuarioRepository {
  salvar(usuario: Usuario): void;
}

class CadastrarUsuario {
  constructor(private repo: UsuarioRepository) {}

  executar(dados: any) {
    // ... lógica de negócio ...
    this.repo.salvar(novoUsuario);
  }
}
```

**Camada Externa (Infraestrutura/Banco):**
```typescript
// O banco de dados se adapta ao que o Caso de Uso pediu.
class MongoDBUsuarioRepository implements UsuarioRepository {
  salvar(usuario: Usuario) {
    // lógica específica do MongoDB
  }
}
```

## 3. Por que isso é importante?

1.  **Testabilidade:** Você pode testar suas regras de negócio sem precisar ligar um banco de dados real (basta usar um "Mock" da interface).
2.  **Facilidade de Troca:** Se amanhã você quiser trocar o MongoDB pelo Postgres, você só precisa criar uma nova classe na camada externa. O núcleo do sistema (Caso de Uso) permanece intacto.
3.  **Independência de Framework:** Você pode trocar o Express pelo Fastify sem tocar em uma única linha de lógica de negócio.

---
**Links Relacionados:**
- [[Clean Architecture]]
- [[Detalhamento das Camadas (Entities e Use Cases)]]
