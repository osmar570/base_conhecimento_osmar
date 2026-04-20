# Ferramentas do Ecossistema Terraform (Lint e Segurança)

Escrever código HCL é apenas o primeiro passo. Para garantir que sua infraestrutura seja profissional, padronizada e segura, você deve utilizar ferramentas que automatizam a revisão do código antes mesmo dele chegar à nuvem.

## 1. `terraform fmt` (Formatação)

O Terraform possui um formatador nativo que garante que todos os arquivos `.tf` sigam o mesmo padrão estético (espaçamento, alinhamento de colunas, etc.).

*   **Por que usar:** Evita discussões em Pull Requests sobre estilo de código e mantém o projeto limpo.
*   **Comando:** `terraform fmt -recursive` (formata todos os arquivos no diretório e subdiretórios).
*   **Dica:** Configure seu editor (VS Code/IntelliJ) para rodar este comando automaticamente ao salvar o arquivo.

## 2. `tflint` (Linter de Código)

Enquanto o comando `terraform validate` verifica apenas a sintaxe básica, o **tflint** vai além e verifica erros específicos dos provedores de nuvem.

*   **O que ele detecta:**
    *   Uso de tipos de instâncias que não existem na região selecionada.
    *   Nomes de recursos que violam regras de nomenclatura da nuvem.
    *   Declaração de variáveis que não estão sendo usadas.
*   **Instalação:** Via Homebrew, Chocolatey ou binário direto.
*   **Comando:** `tflint` no diretório raiz.

## 3. `tfsec` (Segurança e Compliance)

O **tfsec** é um analisador estático focado em segurança. Ele escaneia seu código em busca de configurações que possam expor sua infraestrutura a ataques.

*   **O que ele detecta:**
    *   Bancos de dados abertos para o mundo (`0.0.0.0/0`).
    *   Buckets S3 sem criptografia ativada.
    *   Uso de protocolos inseguros (como HTTP em vez de HTTPS).
    *   Segredos (senhas/chaves) expostos no código.
*   **Comando:** `tfsec .`
*   **Alternativa:** O **Checkov** é uma ferramenta similar e muito popular que também suporta Kubernetes e Docker.

## 4. Integração em CI/CD

Em um fluxo de trabalho profissional, essas ferramentas rodam automaticamente em cada Pull Request:

1.  **Checkout:** Baixa o código.
2.  **Format Check:** `terraform fmt -check` (falha se o código não estiver formatado).
3.  **Lint:** `tflint` (falha se houver erros de lógica/nuvem).
4.  **Security Scan:** `tfsec` (falha se houver riscos de segurança).
5.  **Plan:** `terraform plan` (mostra o que será alterado).

Essa "esteira de testes" garante que nenhuma infraestrutura insegura ou mal formatada seja aplicada em produção.

---
**Links Relacionados:**
- [[Terraform]]
- [[Segurança e Gestão de Segredos]]
- [[Boas Práticas e Otimização]] (Conceitos similares no Docker)
