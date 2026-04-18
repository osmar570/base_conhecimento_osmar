# Arquitetura e Comandos do Terraform

O ciclo de vida de um projeto Terraform segue um fluxo de trabalho padrão chamado **"The Core Workflow"**.

## 1. Os 4 Comandos Principais

### `terraform init`
O primeiro comando que você roda. Ele baixa os **Providers** necessários (ex: os plugins da AWS) e prepara o diretório para trabalhar.

### `terraform plan`
O comando de "visualização". O Terraform compara o seu código com o que existe na nuvem e mostra um relatório:
*   `+` o que será criado.
*   `~` o que será modificado.
*   `-` o que será deletado.
**Dica:** Sempre rode o `plan` e revise antes de aplicar qualquer coisa.

### `terraform apply`
O comando de execução. Ele realmente cria os recursos na nuvem. Ele pedirá uma confirmação final antes de agir.

### `terraform destroy`
Remove **toda** a infraestrutura definida naquele projeto. Use com extremo cuidado.

---

## 2. A Linguagem HCL (HashiCorp Configuration Language)

O código do Terraform é escrito em `.tf`. Ele é feito para ser fácil de ler por humanos.

**Exemplo de sintaxe:**
```hcl
resource "google_compute_instance" "meu_servidor" {
  name         = "web-server"
  machine_type = "e2-medium"
  zone         = "us-central1-a"

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }
}
```
*   `resource`: O tipo de bloco.
*   `google_compute_instance`: O tipo do recurso (definido pelo provider).
*   `meu_servidor`: O nome **interno** que você dá ao recurso no código.
*   `name`: O nome **real** que o servidor terá no Google Cloud.

## 3. O Arquivo de Estado (State)

O arquivo `terraform.tfstate` é gerado automaticamente. 
*   **Atenção:** Nunca edite este arquivo manualmente.
*   **Segurança:** Este arquivo pode conter dados sensíveis (senhas de banco de dados). Em equipes, ele deve ser guardado em um local remoto seguro (como um bucket S3 ou Google Cloud Storage) e nunca no Git.

---
**Links Relacionados:**
- [[O que é Terraform e IaC]]
- [[Estrutura de Projeto e Exemplos]]
