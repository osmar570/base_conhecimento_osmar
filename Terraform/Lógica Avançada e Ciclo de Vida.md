# Lógica Avançada e Ciclo de Vida no Terraform

O Terraform oferece ferramentas para controlar a criação dinâmica de recursos e proteger a integridade da infraestrutura contra remoções acidentais.

## 1. Meta-Arguments: `count` e `for_each`

Estes argumentos permitem criar múltiplos recursos a partir de um único bloco de código.

### A. `count` (Repetição Simples)
Útil quando você quer múltiplos recursos idênticos.
```hcl
resource "aws_instance" "servidores" {
  count         = 3 # Cria 3 instâncias
  ami           = "ami-xyz"
  instance_type = "t2.micro"

  tags = {
    Name = "Servidor-${count.index}" # Servidor-0, Servidor-1, Servidor-2
  }
}
```

### B. `for_each` (Repetição por Mapa/Set)
Mais poderoso que o `count`. Permite criar recursos com base em uma lista de nomes ou configurações específicas.
```hcl
variable "usuarios" {
  default = ["joao", "maria", "osmar"]
}

resource "aws_iam_user" "equipe" {
  for_each = toset(var.usuarios)
  name     = each.value
}
```

## 2. O Bloco `lifecycle` (Proteção de Recursos)

O bloco `lifecycle` controla como o Terraform lida com a criação e destruição dos recursos.

### `prevent_destroy` (O "Seguro de Vida")
Impede que o Terraform destrua o recurso, mesmo que você rode `terraform destroy`.
*   **Quando usar:** Bancos de dados de produção, buckets de logs, redes principais.
```hcl
resource "aws_db_instance" "producao" {
  # ... config do banco ...
  lifecycle {
    prevent_destroy = true
  }
}
```

### `create_before_destroy`
Inverte a lógica padrão. O Terraform primeiro cria o novo recurso e, se der certo, deleta o antigo.
*   **Quando usar:** Recursos que não podem ter downtime durante uma atualização (ex: certificados SSL, grupos de segurança).
```hcl
lifecycle {
  create_before_destroy = true
}
```

### `ignore_changes`
Diz ao Terraform para ignorar mudanças feitas manualmente fora do código.
*   **Exemplo:** Ignorar mudanças no tamanho de um cluster de autoscaling feitas pelo próprio provedor de nuvem.

## 3. Ordem de Execução: `depends_on`

O Terraform geralmente descobre a ordem sozinho. Mas às vezes você precisa forçar uma sequência.
*   **Exemplo:** Garantir que a Rede (VPC) esteja pronta antes de tentar criar o Banco de Dados.

```hcl
resource "aws_db_instance" "meu_banco" {
  # ... config ...
  
  # Força o banco a esperar a rede estar 100% pronta
  depends_on = [aws_vpc.rede_principal]
}
```

## 4. Resumo de Uso

| Recurso | Função Principal |
| :--- | :--- |
| **`count`** | Criar X recursos numerados. |
| **`for_each`** | Criar recursos a partir de uma lista/mapa de nomes. |
| **`prevent_destroy`** | Bloqueia a deleção acidental de recursos críticos. |
| **`depends_on`** | Define manualmente quem deve ser criado primeiro. |

---
**Links Relacionados:**
- [[Terraform]]
- [[Estrutura de Projeto e Exemplos]] (Uso de variáveis com for_each)
- [[Segurança no Docker]] (Princípios de proteção de dados)
