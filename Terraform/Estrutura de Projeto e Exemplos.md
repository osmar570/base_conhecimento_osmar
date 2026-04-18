# Estrutura de Projeto e Exemplos

Projetos Terraform seguem uma estrutura de arquivos padronizada para facilitar a manutenção e o reaproveitamento de código.

## 1. Estrutura de Arquivos Padrão

Embora você possa colocar tudo em um único arquivo, a boa prática é separar assim:

*   **`main.tf`**: Onde você define os recursos principais (o coração do projeto).
*   **`variables.tf`**: Onde você define os parâmetros que podem mudar (ex: o tamanho da máquina, a região).
*   **`outputs.tf`**: Onde você pede para o Terraform mostrar informações úteis após a criação (ex: o IP do servidor criado).
*   **`providers.tf`**: Configuração dos provedores (AWS, GCP, etc.) e versões.
*   **`terraform.tfvars`**: Onde você coloca os **valores** reais das suas variáveis (Este arquivo **NUNCA** deve ir para o Git se tiver senhas).

---

## 2. Exemplo Prático: Criando um Cluster GKE (Simplificado)

Este é um modelo de como seria o código para criar um cluster Kubernetes no Google Cloud:

```hcl
# main.tf
resource "google_container_cluster" "meu_cluster" {
  name     = var.cluster_name
  location = var.region

  # Criando um cluster básico com 1 nó
  initial_node_count = 1

  node_config {
    machine_type = "e2-medium"
  }
}

# variables.tf
variable "cluster_name" {
  description = "Nome do cluster Kubernetes"
  default     = "k8s-producao"
}

variable "region" {
  default = "us-central1"
}

# outputs.tf
output "cluster_endpoint" {
  value = google_container_cluster.meu_cluster.endpoint
}
```

---

## 3. Módulos (Modules)

Conforme seu projeto cresce, você usa **Módulos**. Eles são como "funções" no Terraform.
*   Você cria um módulo chamado `rede`.
*   Sempre que precisar de uma rede nova, você chama o módulo e passa apenas o nome e o IP.
*   Isso evita repetir código (DRY - Don't Repeat Yourself).

## 4. Boas Práticas Cruciais

1.  **Use Variáveis:** Nunca deixe valores fixos ("hardcoded") no `main.tf`. Use o `variables.tf`.
2.  **Remote Backend:** Em projetos reais, configure o Terraform para salvar o arquivo de `state` na nuvem, para que outras pessoas do time possam trabalhar no mesmo projeto.
3.  **Tags:** Sempre coloque tags em seus recursos (ex: `Environment = "Production"`, `Owner = "Osmar"`). Isso ajuda muito na hora de ver a conta no final do mês.
4.  **Versionamento:** Trate seu código Terraform como código de software. Use Git, faça Pull Requests e revise as mudanças.

---
**Links Relacionados:**
- [[O que é Terraform e IaC]]
- [[Arquitetura e Comandos do Terraform]]
