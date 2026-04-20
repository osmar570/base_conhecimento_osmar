# Estratégia de Testes

Garantir a qualidade e a confiabilidade do software através de um conjunto de práticas e ferramentas automatizadas. Uma estratégia sólida permite refatorações seguras e entregas contínuas (CI/CD) com confiança.

---

## 📐 Pirâmide de Testes (Testing Pyramid)

O conceito fundamental para uma estratégia eficiente é o equilíbrio entre custo, velocidade e abrangência.

1.  **Testes Unitários (Base):**
    *   **Foco:** Pequenas partes isoladas do código (funções, métodos, classes).
    *   **Isolamento:** Não devem tocar em recursos externos (DB, API, Disco).
    *   **Vantagem:** Execução extremamente rápida (milissegundos), baixo custo de manutenção.
    *   **Quantidade:** Deve representar a maior parte da sua suíte de testes.

2.  **Testes de Integração (Meio):**
    *   **Foco:** A interação entre dois ou mais componentes ou serviços (ex: validar se o repositório salva corretamente no banco de dados).
    *   **Vantagem:** Garante que os "contratos" entre as partes do sistema estão sendo respeitados.
    *   **Custo:** Mais lentos e complexos que os unitários.

3.  **Testes E2E - End-to-End (Topo):**
    *   **Foco:** Fluxo completo do ponto de vista do usuário final (simulando interações em UI ou fluxos de API completos).
    *   **Desvantagem:** Lentos, caros de manter e propensos a falhas falsas (*flaky tests*).
    *   **Quantidade:** Apenas para os fluxos mais críticos de negócio (*Happy Path*).

---

## 🏗️ Princípios e Práticas

### O Princípio F.I.R.S.T.
Para que uma suíte de testes seja útil para o desenvolvedor, ela deve seguir estes critérios:
- **Fast:** Testes lentos desencorajam a execução frequente.
- **Independent:** Um teste não deve depender do estado ou resultado de outro.
- **Repeatable:** O resultado deve ser o mesmo em qualquer ambiente (Local, CI, Staging).
- **Self-Validating:** O teste deve retornar um status claro (Pass/Fail) sem análise manual.
- **Thorough/Timely:** Devem cobrir cenários de erro (Edge cases) e ser escritos próximos ao código de produção.

### TDD (Test-Driven Development)
Metodologia de design de código orientada por testes através do ciclo **Red-Green-Refactor**:
1.  **🔴 Red:** Escreva um teste que falha para uma funcionalidade que ainda não existe.
2.  **🟢 Green:** Implemente o código mínimo necessário para fazer o teste passar.
3.  **🔵 Refactor:** Melhore o código (limpeza, padrões) garantindo que o teste continue passando.

### Dublês de Teste (Test Doubles)
Termos essenciais para isolar dependências durante os testes:
- **Stub:** Fornece respostas prontas (hardcoded) para chamadas feitas durante o teste.
- **Mock:** Registra expectativas de chamadas e falha o teste se o método não for chamado como esperado.
- **Spy:** Observa a interação entre os objetos sem necessariamente alterar o comportamento.

---

## 🚀 Integração com o Processo de Desenvolvimento

*   **Shift-Left Testing:** Trazer os testes para o início do desenvolvimento (fase de design e implementação).
*   **Gate de CI:** Nenhuma branch deve ser mesclada sem que 100% dos testes passem automaticamente.
*   **Cobertura de Testes (Coverage):** Uma métrica útil, mas perigosa; 100% de cobertura não significa 0 bugs, mas sim que todas as linhas foram executadas.

---
**Links Relacionados:**
- [[Clean Architecture]] (Como estruturar o código para facilitar testes)
- [[GitOps e CD Moderno]] (Onde os testes automatizados são executados no pipeline)
- [[Versão Semântica (SemVer)]] (Testes garantem que mudanças não quebrem compatibilidade)
