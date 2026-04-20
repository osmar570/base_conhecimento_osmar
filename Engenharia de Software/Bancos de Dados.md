# Bancos de Dados e Persistência de Dados

A persistência de dados é um dos pilares mais críticos de qualquer sistema. A escolha do banco de dados certo depende do volume de dados, da complexidade das consultas e das garantias de consistência necessárias.

---

## 🗺️ O Teorema CAP
Fundamental para entender sistemas distribuídos e bancos de dados modernos. Ele afirma que é impossível para um sistema distribuído fornecer simultaneamente mais de duas das seguintes garantias:

1.  **C - Consistency (Consistência):** Todos os nós veem os mesmos dados ao mesmo tempo.
2.  **A - Availability (Disponibilidade):** Toda requisição recebe uma resposta (sucesso ou falha).
3.  **P - Partition Tolerance (Tolerância a Partição):** O sistema continua operando mesmo que haja falha de rede entre os nós.

**Na prática:** Como falhas de rede (P) são inevitáveis na nuvem, você deve escolher entre **Consistência (CP)** ou **Disponibilidade (AP)** durante uma falha.

---

## 🏛️ SQL vs. NoSQL

### Bancos de Dados Relacionais (SQL)
- **Estrutura:** Tabelas com esquemas rígidos e relações (Foreign Keys).
- **Garantias:** Seguem o modelo **ACID** (Atomicity, Consistency, Isolation, Durability).
- **Escalabilidade:** Geralmente Vertical (aumentar CPU/RAM). Escala horizontal é complexa (Read Replicas, Sharding).
- **Exemplos:** PostgreSQL, MySQL, SQL Server.
- **Uso ideal:** Dados estruturados, transações financeiras, sistemas ERP/CRM.

### Bancos de Dados Não-Relacionais (NoSQL)
- **Estrutura:** Flexível (Documentos, Chave-Valor, Grafos, Colunares).
- **Garantias:** Seguem o modelo **BASE** (Basically Available, Soft state, Eventual consistency).
- **Escalabilidade:** Projetados para escala Horizontal (adicionar mais servidores).
- **Exemplos:** MongoDB (Documentos), Redis (Chave-Valor), Cassandra (Colunar), Neo4j (Grafos).
- **Uso ideal:** Big Data, catálogos de produtos, redes sociais, sistemas de cache.

---

## 🔄 Consistência Eventual vs. Forte
- **Consistência Forte:** O dado é atualizado em todos os nós antes da confirmação. Se você escreve e lê imediatamente, verá o dado novo.
- **Consistência Eventual:** O sistema garante que, se não houver novas atualizações, eventualmente todos os nós terão o dado mais recente. Muito comum em sistemas AP (Disponibilidade + Partição).

---

## ⚙️ Migrations: O Versionamento do Banco
Assim como o código é versionado no Git, o esquema do banco de dados deve ser versionado através de **Migrations**.
- **O que são:** Scripts (geralmente SQL ou código) que descrevem alterações incrementais no banco (ex: `add_column_email_to_users`).
- **Por que usar:** Garante que todos os desenvolvedores e ambientes (Dev, Staging, Prod) tenham a mesma estrutura de banco, evitando o famoso "na minha máquina funciona".

---
**Links Relacionados:**
- [[Docker]] (Persistência de dados com Volumes)
- [[Kubernetes]] (StatefulSets para bancos de dados em container)
- [[Clean Architecture]] (Onde o banco de dados é apenas um detalhe de infraestrutura)
- [[Design de APIs]] (Idempotência e transações)
