# Terraform Backend Remoto e State Locking

Por padrão, o Terraform salva o estado da infraestrutura em um arquivo local chamado `terraform.tfstate`. Em ambientes profissionais e equipes, isso é um problema de segurança e colaboração. A solução é o **Backend Remoto**.

## 1. O Problema do Estado Local

1.  **Colaboração:** Se você e um colega trabalham no mesmo projeto, cada um terá um arquivo de estado diferente em sua máquina.
2.  **Segurança:** O arquivo de estado contém informações sensíveis (senhas, chaves de API) em texto plano.
3.  **Corrupção de Dados:** Se duas pessoas rodarem `terraform apply` ao mesmo tempo, o estado pode ser corrompido.

## 2. Backend Remoto (S3 e GCS)

O Backend Remoto move o arquivo de estado para a nuvem.

### Exemplo: AWS S3
Para usar o S3, você define um bloco `backend` dentro do bloco `terraform`:

```hcl
terraform {
  backend "s3" {
    bucket         = "nome-do-seu-bucket-de-estado"
    key            = "projetos/infra-producao.tfstate"
    region         = "us-east-1"
    encrypt        = true # Sempre use criptografia
  }
}
```

### Exemplo: Google Cloud Storage (GCS)
```hcl
terraform {
  backend "gcs" {
    bucket  = "nome-do-seu-bucket-gcs"
    prefix  = "terraform/state"
  }
}
```

## 3. State Locking com DynamoDB (AWS)

Mesmo com o estado na nuvem, duas pessoas podem tentar rodar o comando ao mesmo tempo. O **State Locking** resolve isso criando um "cadeado" temporário.

Na AWS, usamos uma tabela do **DynamoDB** para isso:

1.  O Terraform tenta rodar o `apply`.
2.  Ele escreve uma entrada na tabela DynamoDB dizendo: "Estou usando este estado agora".
3.  Se outra pessoa tentar rodar, o Terraform verá o registro no DynamoDB e retornará um erro: *"Error: Error acquiring the state lock"*.

### Configuração Completa (S3 + DynamoDB):

```hcl
terraform {
  backend "s3" {
    bucket         = "osmar-infra-state"
    key            = "network/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-lock-table" # Nome da tabela para o cadeado
  }
}
```
*Nota: A tabela DynamoDB deve ter uma **Partition Key** chamada `LockID` do tipo String.*

## 4. Fluxo de Configuração

1.  **Crie os recursos manualmente (ou via script):** Você precisa que o Bucket e a Tabela DynamoDB existam **antes** de configurar o backend.
2.  **Adicione o bloco `backend`** no seu arquivo `providers.tf` ou `main.tf`.
3.  **Rode `terraform init`:** O Terraform detectará a mudança e perguntará se você deseja copiar o estado local existente para o novo backend remoto. Digite `yes`.

## 5. Boas Práticas

*   **Versionamento do Bucket:** Ative o versionamento no seu Bucket S3/GCS. Se o estado for corrompido, você pode voltar para uma versão anterior do arquivo.
*   **Múltiplos Estados:** Não coloque toda a sua empresa em um único arquivo de estado. Separe por ambiente ou serviço (ex: `network.tfstate`, `database.tfstate`).

---
**Links Relacionados:**
- [[Terraform]]
- [[Arquitetura e Comandos do Terraform]]
- [[Segurança no Docker]] (Conceitos de segurança de dados)
