# Licenças de Software

Escolher a licença correta é fundamental para definir como outros podem usar, modificar e distribuir o seu código. No mundo Open Source, as licenças se dividem principalmente entre **Permissivas** e **Copyleft**.

---

## 1. Licenças Permissivas
Permitem que o código seja usado quase sem restrições, inclusive em softwares proprietários.

### MIT License
A mais popular e simples.
*   **Permite:** Uso comercial, modificação, distribuição e uso privado.
*   **Exigência:** Incluir o aviso de copyright original.
*   **Exemplo:** React, Vue, Node.js.

### Apache License 2.0
Similar à MIT, mas oferece proteção explícita sobre **Patentes**.
*   **Permite:** Uso comercial e modificações.
*   **Vantagem:** Garante que quem contribui com o código não possa processar o usuário por uso de patentes contidas naquela contribuição.
*   **Exemplo:** Kubernetes, Terraform, Android.

### BSD (2-Clause e 3-Clause)
Muito similar à MIT, focada na liberdade total de uso e redistribuição.

---

## 2. Licenças Copyleft (Restritivas)
Baseiam-se no princípio de que qualquer software derivado também deve ser Open Source.

### GNU GPL v3 (General Public License)
A licença "viral" mais famosa.
*   **Regra de Ouro:** Se você modificar um software sob GPL e distribuí-lo, o seu código também **deve ser aberto sob a mesma licença (GPL)**.
*   **Uso:** Muito comum em projetos que querem garantir que o conhecimento continue livre para sempre.
*   **Exemplo:** Linux Kernel (v2), Git, GIMP.

---

## 3. Licenças para a Nuvem (SaaS)

### AGPL (Affero GPL)
Criada para fechar uma brecha da GPL. Se o software roda apenas em um servidor (SaaS) e o código não é "distribuído" para o PC do usuário, a GPL normal não obriga a abertura do código. A AGPL obriga a abertura mesmo se o uso for apenas via rede.
*   **Exemplo:** MongoDB (usava antigamente), Grafana (versões específicas).

---

## 4. Software Proprietário
O código pertence a uma empresa ou indivíduo e não pode ser copiado, modificado ou distribuído sem autorização explícita e, geralmente, pagamento.

---

## ⚖️ Resumo: Qual escolher?

| Se você quer... | Use a Licença... |
| :--- | :--- |
| Simplicidade e máxima adoção | **MIT** |
| Proteção contra processos de patentes | **Apache 2.0** |
| Garantir que o código continue sempre livre | **GPL v3** |
| Cobrar pelo uso e esconder o código | **Proprietária** |

---
**Links Relacionados:**
- [[Engenharia de Software]] (Índice)
- [[Git]] (Onde o arquivo LICENSE reside)
