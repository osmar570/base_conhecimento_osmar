# Base de Conhecimento - Docker & Kubernetes

Este repositório é um **Vault do Obsidian** focado em documentação técnica e notas de estudo sobre tecnologias cloud-native, especificamente Docker e Kubernetes.

## 📂 Visão Geral do Diretório

O projeto está organizado em dois pilares principais:

### 🐳 Docker (`/Docker`)
Contém notas fundamentais e técnicas sobre conteinerização.
- **Introdução ao Docker e Conteinerização.md**: Guia inicial, problemas resolvidos e trilha de aprendizagem.
- **O que são Containers (Detalhes Técnicos).md**: Explicação profunda sobre Namespaces, Cgroups, Layered File System e Runtime.
- **O que é uma Imagem Docker.md**: Detalhes sobre a construção e estrutura de imagens.
- **Docker Compose.md**: Gerenciamento de stacks multi-container.
- **Boas Práticas e Otimização.md**: Multi-stage builds, cache de camadas e .dockerignore.
- **Redes no Docker.md**: Drivers de rede (Bridge, Host, Overlay) e comunicação DNS.
- **Segurança no Docker.md**: Usuário root, limites de recursos e imagens oficiais.
- **Troubleshooting no Docker.md**: Exit codes, docker inspect, stats e limpeza de ambiente.
- **Orquestração com Kubernetes.md**: Transição do Docker para orquestradores.

### ☸️ Kubernetes (`/Kubernetes`)
Uma coleção abrangente de guias e conceitos sobre orquestração de containers.
- **Kubernetes.md**: Visão geral e conceitos fundamentais do K8s.
- **Troubleshooting no Kubernetes.md**: Fluxo de depuração, estados de erro (CrashLoop, OOM) e comandos de inspeção.
- **RBAC e Governança.md**: Roles, ServiceAccounts, ResourceQuotas e segurança baseada em privilégio mínimo.
- **GitOps e CD Moderno.md**: Princípios de reconciliação contínua, Push vs Pull e ferramentas (ArgoCD/Flux).
- **Guia Prático de GitOps.md**: Instalação do Argo CD, definição de Applications e monitoramento de sincronia.
- **Estratégias de Deployment.md**: Rolling Update, Recreate, Blue/Green e Canary.
- **como iniciar (Local).md**: Guia prático para Minikube, K3s e MicroK8s.
- **como iniciar (GKE).md** & **Gerenciamento de Nodes (GKE)**: Notas específicas sobre Google Kubernetes Engine.
- **Manifestos YAML e Persistência.md**: Exploração de recursos declarativos.
- **Helm - Gerenciador de Pacotes.md**: Automação de deployments.
- **Gateway API e HTTPRoute.md**: Evolução do Ingress, separação de papéis e roteamento avançado.
- **Service Mesh - Istio.md** : Tópicos avançados de comunicação.

### 🏗️ Terraform (`/Terraform`)
Documentação sobre Infraestrutura como Código (IaC).
- **Terraform.md**: Conceitos fundamentais, Providers e o arquivo de State.
- **Arquitetura e Comandos do Terraform.md**: O ciclo de vida (Init, Plan, Apply, Destroy) e linguagem HCL.
- **Backend Remoto e State Locking.md**: Colaboração em equipe, S3, GCS e travas com DynamoDB.
- **Lógica Avançada e Ciclo de Vida.md**: Meta-arguments (count, for_each), proteção de recursos e depends_on.
- **Workspaces e Ambientes.md**: Estratégias para Dev, Staging e Prod usando workspaces ou pastas.
- **Terraform Import.md**: Como trazer infraestrutura existente para o controle do código.
- **Segurança e Gestão de Segredos.md**: Integração com Secret Managers, variáveis sensitive e proteção do State.
- **Ferramentas do Ecossistema.md**: terraform fmt, tflint e auditoria de segurança com tfsec.
- **Estrutura de Projeto e Exemplos.md**: Organização de arquivos (.tf), variáveis, módulos e exemplo de GKE.
- **Exemplo Completo - K8s, Rancher e Gateway API.md**: Guia prático provisionando Ubuntu, K3s, Rancher via Helm e rotas Gateway API.
- **Monitoramento e Autoscaling**: Práticas de observabilidade e escalabilidade.

## 🚀 Como utilizar

Este repositório foi projetado para ser visualizado no **Obsidian**, aproveitando os links internos (`[[Link]]`) entre as notas.

1.  **Exploração**: Comece pelos arquivos `Docker/Docker.md` ou `Kubernets/Kubernetes.md` para uma introdução aos tópicos.
2.  **Referência Rápida**: Utilize a pasta `Kubernets` para comandos essenciais e configurações de objetos fundamentais (Pods, Services, ConfigMaps).
3.  **Ambientes**: Existem guias específicos para configuração local (Minikube/K3s) e em nuvem (GKE/AKS/OKE).

## 🛠️ Convenções
- As notas estão escritas em **Português (PT-BR)**.
- Utiliza-se a sintaxe padrão de Markdown com extensões do Obsidian (como WikiLinks).
- O nome da pasta `Kubernets` (sic) é mantido conforme a estrutura original do projeto.
