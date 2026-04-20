# SemVer (Semantic Versioning)

O **Versionamento Semântico (SemVer)** é um conjunto de regras que define como os números de versão de um software devem ser atribuídos e incrementados. O objetivo é tornar a evolução do software previsível para os desenvolvedores que dependem dele.

---

## 1. A Estrutura: X.Y.Z

Um número de versão no padrão SemVer deve seguir o formato **MAJOR.MINOR.PATCH** (ex: `2.4.1`):

### **MAJOR (X): Versão Maior**
Incrementada quando você faz alterações de API **incompatíveis** (quebras de contrato). 
*   **Ação:** Usuários precisam alterar o código deles para atualizar para esta versão.

### **MINOR (Y): Versão Menor**
Incrementada quando você adiciona funcionalidades de maneira **compatível** com as versões anteriores.
*   **Ação:** Novos recursos são adicionados, mas o código antigo continua funcionando normalmente.

### **PATCH (Z): Versão de Correção**
Incrementada quando você faz apenas **correções de bugs** (bug fixes) compatíveis com as versões anteriores.
*   **Ação:** Nenhuma mudança de comportamento, apenas melhorias de estabilidade ou segurança.

---

## 2. Versões de Pré-lançamento

Você pode adicionar um hífen e um identificador para versões que ainda não estão prontas para produção:
*   `1.0.0-alpha` (Fase inicial de testes)
*   `1.0.0-beta.1` (Funcionalidades completas, mas com bugs conhecidos)
*   `1.0.0-rc.1` (Release Candidate: quase pronto para o lançamento oficial)

---

## 3. A Importância em Gerenciadores de Pacotes

Gerenciadores como `npm`, `nuget` ou `pip` usam o SemVer para decidir quais atualizações baixar:
*   `^1.2.3`: Aceita qualquer versão até a `1.9.9` (todas as MINOR e PATCH compatíveis).
*   `~1.2.3`: Aceita apenas correções (PATCH), travando na `1.2.x`.

---

## 4. Relação com Conventional Commits

O SemVer e os [[Conventional Commits e Commit Lint|Conventional Commits]] trabalham juntos para automação:
*   Commits do tipo `fix` geram um incremento no **PATCH**.
*   Commits do tipo `feat` geram um incremento no **MINOR**.
*   Commits com `BREAKING CHANGE` geram um incremento no **MAJOR**.

---

## 💡 Regra de Ouro: Versão 0.y.z
Softwares na versão `0.x.x` são considerados em **desenvolvimento inicial**. A API pode mudar a qualquer momento sem aviso prévio. O SemVer "real" começa a valer a partir da versão `1.0.0`.

---
**Links Relacionados:**
- [[Engenharia de Software]] (Índice)
- [[Git/Conventional Commits e Commit Lint]]
- [[Linux/Gerenciamento de Pacotes]]
