# Terraform Import

O **Terraform Import** é o comando utilizado para colocar recursos que já existem (criados manualmente via console ou via CLI) sob a gestão do Terraform, sem precisar destruí-los e recriá-los.

## 1. Por que usar o Import?

Muitas vezes, começamos a usar Terraform em uma infraestrutura que já tem anos de existência. 
*   **Evita Downtime:** Você não precisa deletar o servidor de produção para começar a gerenciá-lo via código.
*   **Consistência:** Garante que recursos antigos sigam as mesmas regras e padrões dos novos.

## 2. O Fluxo de Trabalho (Workflow)

É importante entender que o `terraform import` **não gera o código `.tf` sozinho**. Ele apenas atualiza o arquivo de **Estado (State)**.

### Passo 1: Escreva o Código
Crie um bloco de recurso no seu arquivo `main.tf` que corresponda ao que você quer importar. Não precisa ser perfeito agora, você pode ajustar depois.
```hcl
resource "aws_instance" "servidor_antigo" {
  # Deixe os atributos em branco ou com valores genéricos por enquanto
}
```

### Passo 2: Execute o Comando Import
Você precisa do **ID do recurso** no provedor de nuvem (ex: o ID da instância EC2 ou o nome do bucket S3).
```bash
terraform import aws_instance.servidor_antigo i-0123456789abcdef0
```

### Passo 3: Sincronize o Código (O segredo do sucesso)
Após o import, o seu **Estado** tem as informações reais, mas o seu **Código** ainda está vazio ou incompleto.
1.  Rode `terraform plan`.
2.  O Terraform mostrará uma lista enorme de diferenças (atributos que estão no estado mas não no seu código).
3.  Vá copiando esses atributos do terminal para o seu arquivo `.tf` até que o `terraform plan` retorne: *"No changes. Your infrastructure matches the configuration."*

## 3. Exemplos Comuns

*   **Bucket S3:**
    `terraform import aws_s3_bucket.bucket_backup meu-bucket-de-logs-antigo`
*   **Grupo de Segurança (Security Group):**
    `terraform import aws_security_group.sg_web sg-0a1b2c3d4e5f`
*   **Usuário IAM:**
    `terraform import aws_iam_user.admin osmar-admin`

## 4. Limitações Importantes

1.  **Não gera código:** Como mencionado, você ainda tem que escrever o HCL manualmente.
2.  **Um por um:** O comando padrão importa apenas um recurso por vez.
3.  **Complexidade:** Recursos complexos (como clusters Kubernetes inteiros) podem exigir a importação de muitos sub-recursos manualmente.

## 5. Dica de Especialista: `import` block (Terraform 1.5+)

Nas versões mais recentes, o Terraform introduziu o bloco `import`, que permite declarar a intenção de importar diretamente no código:

```hcl
import {
  to = aws_instance.servidor_antigo
  id = "i-0123456789abcdef0"
}
```
Isso permite que o Terraform ajude a gerar o código base para você usando o comando `terraform plan -generate-config-out=gerado.tf`.

---
**Links Relacionados:**
- [[Terraform]]
- [[Arquitetura e Comandos do Terraform]]
- [[Backend Remoto e State Locking]]
