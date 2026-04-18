# Terraform e Infraestrutura como Código (IaC)

O **Terraform** é uma ferramenta de **Infraestrutura como Código (IaC)** criada pela HashiCorp. Ela permite que você defina sua infraestrutura (servidores, redes, firewalls, etc.) usando arquivos de configuração simples e legíveis, em vez de clicar manualmente em painéis de nuvem (como o console da AWS ou GCP).

## 1. O que é IaC?

Imagine que você precisa de 3 servidores, 1 banco de dados e 1 rede. 
*   **Sem IaC:** Você abre o navegador, faz login no Google Cloud, clica em "Criar Instância", preenche 20 campos, repete isso 3 vezes. Se precisar de outro ambiente igual amanhã, terá que lembrar de todos os cliques.
*   **Com IaC:** Você escreve um arquivo de texto descrevendo esses recursos. O Terraform lê esse arquivo e cria tudo para você. Se precisar de outro ambiente, basta rodar o mesmo arquivo.

## 2. Como o Terraform funciona?

O Terraform é **Declarativo**. Você diz o que quer (ex: "Quero um cluster Kubernetes com 3 nós"), e o Terraform descobre **como** chegar lá.

### Os 3 Pilares do Terraform:

1.  **Providers (Provedores):** São "plugins" que permitem ao Terraform falar com diferentes nuvens ou serviços (AWS, GCP, Azure, DigitalOcean, Cloudflare e até o próprio Docker/Kubernetes).
2.  **Resources (Recursos):** É o que você quer criar. Um servidor, um IP fixo, um disco rígido.
3.  **State (Estado):** É o cérebro do Terraform. Ele guarda um arquivo (`terraform.tfstate`) que mapeia o que está no seu código com o que existe no mundo real. Se você mudar um servidor no código, o Terraform olha o State, vê que o servidor real é diferente e decide se deve atualizá-lo ou recriá-lo.

## 3. Por que usar Terraform com Kubernetes?

Embora o Kubernetes gerencie seus Pods, o **Terraform gerencia o Cluster em si**. 
*   Você usa o Terraform para criar o cluster GKE (Google Kubernetes Engine).
*   Depois que o cluster existe, você usa o Helm ou Kubernetes Manifests (ou o próprio Terraform) para colocar as aplicações lá dentro.

---
**Próximos Passos:**
- [[Arquitetura e Comandos do Terraform]]
- [[Estrutura de Projeto e Exemplos]]
