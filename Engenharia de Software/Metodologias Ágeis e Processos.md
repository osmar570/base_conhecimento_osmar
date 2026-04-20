# Metodologias Ágeis e Processos de Desenvolvimento

O desenvolvimento ágil busca entregar valor de forma incremental e contínua, utilizando ciclos curtos de feedback para se adaptar a mudanças e imprevistos.

---

## 🏎️ Scrum: Gestão por Iterações
O Scrum organiza o trabalho em ciclos fixos chamados **Sprints**.

### Papéis (Roles)
- **Product Owner (PO):** Define as prioridades do negócio (o "quê").
- **Scrum Master:** Garante que o time siga o processo e remove barreiras.
- **Time de Desenvolvimento:** Multidisciplinar e auto-organizado (o "como").

### Cerimônias
1. **Planning:** O que cabe na próxima Sprint?
2. **Daily:** 15 minutos para alinhar o dia e identificar bloqueios.
3. **Review:** Apresentação do software funcionando para os stakeholders.
4. **Retrospective:** O que o time pode melhorar no processo para a próxima Sprint?

---

## 🌊 Kanban: Gestão de Fluxo Contínuo
O Kanban foca na visualização e na otimização do fluxo de trabalho sem iterações fixas.

### Princípios Técnicos
- **Visualizar o Trabalho:** Uso de quadros (Boards).
- **Limitar o WIP (Work In Progress):** O segredo do Kanban. Limitar quantas tarefas podem estar em uma coluna ao mesmo tempo para evitar gargalos e multitasking.
- **Métricas de Fluxo:**
    - **Lead Time:** Tempo total desde a solicitação até a entrega.
    - **Cycle Time:** Tempo que o time levou trabalhando ativamente na tarefa.

---

## 🛠️ Práticas de Engenharia Ágil

### XP (Extreme Programming)
Práticas que garantem a qualidade técnica necessária para a agilidade:
- **Pair Programming:** Revisão de código em tempo real.
- **TDD:** Código guiado por testes (Red-Green-Refactor).
- **Refatoração:** Melhoria contínua da estrutura interna sem mudar o comportamento.

### Estratégias de Versionamento
- **Trunk Based Development:** Foco em merges pequenos e frequentes na branch principal. Evita branches de longa duração que causam conflitos complexos.
- **Feature Flags / Toggles:** Permite o deploy de código em produção que fica "escondido" do usuário até estar pronto para ser ativado.

---

## 🔄 Ciclo de Vida do Software (SDLC)
As metodologias ágeis transformam o SDLC tradicional (Waterfall) em um ciclo contínuo:
`Planejar -> Codificar -> Testar -> Deploy -> Monitorar -> Feedback -> (Repetir)`

---
**Links Relacionados:**
- [[Git]] (Estratégias de branch)
- [[Estratégia de Testes]] (Fundamental para CI e agilidade técnica)
- [[Observabilidade e SRE]] (Feedback de produção para o próximo planejamento)
- [[Versão Semântica (SemVer)]] (Padronização de entregas incrementais)
