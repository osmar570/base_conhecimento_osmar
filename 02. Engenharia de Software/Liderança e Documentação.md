# Liderança Técnica e Documentação

Liderança técnica não é apenas sobre escrever código, mas sobre guiar o time em direção a decisões sustentáveis e garantir que o conhecimento não se perca no tempo.

---

## 📝 ADR - Architecture Decision Record

Um ADR é um documento curto que registra uma decisão arquitetural significativa, o contexto em que foi tomada e as consequências dessa escolha.

### Estrutura de um ADR:
1.  **Título:** Identificador claro (ex: `ADR 001: Uso de gRPC para comunicação interna`).
2.  **Status:** Proposto, Aceito, Substituído ou Depreciado.
3.  **Contexto:** Qual problema estamos resolvendo? Quais eram as opções?
4.  **Decisão:** O que escolhemos e por quê.
5.  **Consequências:** O que ganhamos e o que perdemos (trade-offs) com essa escolha.

**Benefício:** Evita discussões repetitivas no futuro ("Por que fizemos assim mesmo?") e ajuda no onboarding de novos membros.

---

## 📉 Gestão de Dívida Técnica

A dívida técnica é o custo de escolher uma solução rápida agora em vez de uma solução melhor que levaria mais tempo.

### Tipos de Dívida:
- **Dívida Prudente:** Assumida deliberadamente para validar um MVP ou cumprir um prazo vital.
- **Dívida Imprudente:** Gerada por falta de conhecimento, falta de testes ou design ruim.

### Como gerenciar:
1.  **Visibilidade:** Registre a dívida no backlog ou em um "Tech Debt Radar".
2.  **Pagamento Contínuo:** Reserve uma porcentagem da Sprint (ex: 20%) para refatoração e melhoria técnica.
3.  **Regra do Escoteiro:** "Deixe o código sempre um pouco mais limpo do que você o encontrou".

---

## 🤝 Liderança Servidora e Mentoria

O papel de um Tech Lead ou Arquiteto é remover barreiras técnicas para o time.
- **Code Review como Ensino:** Use as revisões para explicar o "porquê", não apenas o "o quê".
- **Disseminação de Conhecimento:** Realize *Tech Talks* ou *Pair Programming* para elevar o nível técnico do grupo.

---
**Links Relacionados:**
- [[02. Engenharia de Software/Clean Architecture/Clean Architecture|Clean Architecture]] (O padrão a ser defendido)
- [[05. Trilhas de Estudos/Tech Lead|Trilha de Tech Lead]]
- [[05. Trilhas de Estudos/Arquiteto de Software|Trilha de Arquiteto]]
