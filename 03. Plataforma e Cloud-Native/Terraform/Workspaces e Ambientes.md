# Gerenciamento de Ambientes no Terraform

Uma das maiores necessidades em projetos reais é gerenciar múltiplos ambientes (Ex: Desenvolvimento, Staging e Produção) usando o mesmo código base. Existem duas estratégias principais para isso.

## 1. Terraform Workspaces (Isolamento por Estado)

Workspaces permitem que você use o mesmo diretório de código para gerenciar múltiplos estados separados.

### Como funciona:
O Terraform cria um arquivo de estado (`.tfstate`) diferente para cada workspace. 
*   Você pode acessar o nome do workspace atual usando a variável `${terraform.workspace}` dentro do seu código.

### Comandos Principais:
*   `terraform workspace new dev`: Cria um novo ambiente.
*   `terraform workspace select prod`: Alterna para o ambiente de produção.
*   `terraform workspace list`: Mostra todos os ambientes criados.

### Exemplo de Código Dinâmico:
```hcl
resource "aws_instance" "app" {
  ami           = "ami-xyz"
  # Se o workspace for 'prod', usa uma máquina grande. Se não, usa uma pequena.
  instance_type = terraform.workspace == "prod" ? "t3.large" : "t2.micro"

  tags = {
    Name        = "App-${terraform.workspace}"
    Environment = terraform.workspace
  }
}
```

---

## 2. Estratégia de Pastas Separadas (A mais comum em grandes empresas)

Nesta abordagem, você cria uma estrutura de pastas físicas para cada ambiente. É considerada mais segura e explícita para infraestruturas complexas.

### Estrutura Sugerida:
```text
projeto-infra/
├── modules/           # Código reutilizável (Rede, Cluster, Banco)
│   ├── vpc/
│   └── eks/
├── environments/
│   ├── dev/
│   │   ├── main.tf    # Chama os módulos passando valores de Dev
│   │   └── variables.tf
│   └── prod/
│       ├── main.tf    # Chama os módulos passando valores de Prod
│       └── variables.tf
```

### Por que usar Pastas em vez de Workspaces?
1.  **Isolamento Total:** O backend (Bucket S3) pode ser diferente para cada ambiente (Segurança).
2.  **Configurações Distintas:** Produção pode ter recursos que o ambiente de Dev nem possui (Ex: Multi-AZ, Backups extras).
3.  **Clareza no Code Review:** É mais fácil ver no Git que alguém mudou algo na pasta `prod/` do que uma mudança sutil em uma lógica de workspace.

---

## 3. Resumo: Qual escolher?

| Característica | Workspaces | Pastas Separadas |
| :--- | :--- | :--- |
| **Código** | Exatamente o mesmo | Reutilizado via Módulos |
| **Complexidade** | Baixa | Média |
| **Isolamento de Estado** | No mesmo bucket (prefixos diferentes) | Podem estar em buckets/contas diferentes |
| **Ideal para** | Ambientes idênticos (Ex: Testes efêmeros) | Ambientes com arquiteturas diferentes (Dev vs Prod) |

---
**Links Relacionados:**
- [[Terraform]]
- [[Estrutura de Projeto e Exemplos]] (Conceitos de Módulos)
- [[Backend Remoto e State Locking]]
