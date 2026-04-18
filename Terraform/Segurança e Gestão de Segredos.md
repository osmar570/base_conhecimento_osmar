# Segurança e Gestão de Segredos no Terraform

O maior erro em Projetos de IaC é expor segredos (senhas, chaves de API, certificados) no código fonte. O Terraform deve ser um canal para a infraestrutura, não um repositório de segredos.

## 1. A Regra de Ouro: Nunca no Git

Nunca coloque valores sensíveis diretamente nos seus arquivos `.tf`.
*   **Ameaça:** Uma vez que um segredo é commitado, ele fica no histórico do Git para sempre, mesmo que você o apague depois.
*   **Solução:** Use variáveis e busque os valores de fontes externas seguras.

## 2. Estratégias de Gestão de Segredos

### A. Variáveis de Ambiente
O Terraform busca automaticamente variáveis que começam com `TF_VAR_`.
*   Exemplo: Se você tem uma variável `db_password`, pode definir no terminal:
    `export TF_VAR_db_password="senha_super_secreta"`
*   **Vantagem:** O segredo nunca toca o disco.

### B. Arquivos `.tfvars` (Com Cuidado)
Você pode usar um arquivo `secrets.tfvars`, mas ele **DEVE** estar no seu `.gitignore`.

### C. Secret Managers (Recomendado para Produção)
A forma mais segura é integrar o Terraform com um cofre de senhas (AWS Secrets Manager, Google Secret Manager ou HashiCorp Vault). O Terraform busca o segredo em tempo de execução.

#### Exemplo: Buscando senha do AWS Secrets Manager
```hcl
# 1. Busca a versão mais recente do segredo existente na AWS
data "aws_secretsmanager_secret_version" "db_password" {
  secret_id = "producao/banco-dados/senha"
}

# 2. Usa o valor dentro do recurso do banco
resource "aws_db_instance" "app_db" {
  # ... outras configs ...
  password = data.aws_secretsmanager_secret_version.db_password.secret_string
}
```

## 3. O Atributo `sensitive = true`

Sempre que definir uma variável que contenha dados sensíveis, marque-a como `sensitive`. Isso impede que o Terraform exiba o valor da senha no console durante o `plan` ou `apply`.

```hcl
variable "db_password" {
  type      = string
  sensitive = true
}
```
*   **Resultado:** No terminal, o Terraform mostrará `<sensitive>` em vez da senha real.

## 4. Segurança do Arquivo de Estado (State)

Lembre-se: Mesmo usando Secret Managers, o valor final da senha **ficará gravado no arquivo `terraform.tfstate`** em texto plano.
*   **Por que?** O Terraform precisa saber o valor atual para comparar com mudanças futuras.
*   **Como proteger:**
    1.  **Backend Remoto:** Sempre use S3/GCS com criptografia ativada.
    2.  **Acesso Restrito:** Limite quem pode ler o bucket do estado apenas aos administradores e ao pipeline de CI/CD.

## 5. Ferramentas de Auditoria

*   **tfsec / Chekov:** Escaneiam seu código em busca de segredos expostos ou configurações inseguras (ex: portas abertas, falta de criptografia).
*   **git-secrets / gitleaks:** Impedem que você faça um `git commit` se detectar algo que pareça uma senha ou chave de API no código.

---
**Links Relacionados:**
- [[Terraform]]
- [[Backend Remoto e State Locking]]
- [[Segurança no Docker]]
