# Clean Architecture vs Hexagonal Architecture

Embora tenham nomes diferentes e diagramas distintos, a **Clean Architecture** (Robert C. Martin) e a **Arquitetura Hexagonal** (Alistair Cockburn) buscam o mesmo objetivo: **Independência de tecnologia e testabilidade**.

---

## 1. Arquitetura Hexagonal (Ports and Adapters)

Criada antes da Clean Architecture, ela foca na simetria do sistema. O sistema é um "hexágono" e o mundo exterior se conecta a ele através de **Portas** (Interfaces) e **Adaptadores**.

*   **Lado Esquerdo (Driving Adapters):** Usuários ou sistemas que "dirigem" sua aplicação (ex: Web, CLI).
*   **Lado Direito (Driven Adapters):** Sistemas que sua aplicação "dirige" (ex: Banco de Dados, APIs de Terceiros).
*   **O Núcleo:** Contém apenas a lógica de negócio, sem saber se o tráfego vem de um navegador ou de um teste automatizado.

---

## 2. Clean Architecture

A Clean Architecture é, de certa forma, uma evolução ou uma especialização da Hexagonal. Ela é mais **prescritiva** sobre como organizar o interior do hexágono.

*   **Camadas Definidas:** Enquanto a Hexagonal fala apenas em "Núcleo", a Clean divide esse núcleo em **Entities** e **Use Cases**.
*   **Regra da Dependência:** É muito enfática sobre o sentido das dependências (sempre para o centro).

---

## 3. Comparativo de Termos

| Conceito | Hexagonal Architecture | Clean Architecture |
| :--- | :--- | :--- |
| **Ponto de Entrada** | Driver Adapter (Controller) | Interface Adapter (Controller) |
| **Lógica de Negócio** | Core / Domain | Entities + Use Cases |
| **Abstração de Saída** | Port (Interface) | Gateway / Repository Interface |
| **Acesso a Dados** | Driven Adapter (Repo) | Interface Adapter (Gateway) |

---

## 4. Principais Diferenças e Semelhanças

### Semelhanças (O DNA Comum)
*   **Desacoplamento:** Ambas permitem trocar o banco de dados ou a interface de usuário sem tocar na lógica de negócio.
*   **Testabilidade:** Ambas facilitam testes de unidade isolados de IO.
*   **Uso de Interfaces:** Ambas dependem fortemente do Princípio de Inversão de Dependência ([[Regra da Dependência e DIP|DIP]]).

### Diferenças
*   **Estrutura Interna:** A Clean Architecture é mais rígida sobre as camadas internas (Entities vs Use Cases). A Hexagonal é mais flexível sobre como você organiza o código dentro do hexágono.
*   **Foco Visual:** A Hexagonal foca no **limite** (fronteira) entre a app e o mundo. A Clean foca na **hierarquia** e proteção das regras de negócio.

---

## 5. Qual escolher?

Na prática, a maioria dos desenvolvedores modernos utiliza uma **combinação das duas**:
*   Usa o conceito de **Ports and Adapters** da Hexagonal para organizar a comunicação com o mundo.
*   Usa a divisão de **Entities e Use Cases** da Clean para organizar a lógica de negócio interna.

---
**Links Relacionados:**
- [[Clean Architecture]]
- [[Regra da Dependência e DIP]]
- [[Interface Adapters (Controllers e Gateways)]]
