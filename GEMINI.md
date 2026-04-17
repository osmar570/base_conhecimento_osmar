# Base de Conhecimento - Docker & Kubernetes

Este repositório é um **Vault do Obsidian** focado em documentação técnica e notas de estudo sobre tecnologias cloud-native, especificamente Docker e Kubernetes.

## 📂 Visão Geral do Diretório

O projeto está organizado em dois pilares principais:

### 🐳 Docker (`/Docker`)
Contém notas fundamentais e técnicas sobre conteinerização.
- **Docker.md**: Introdução e conceitos básicos de containers.
- **O que são Containers (Detalhes Técnicos).md**: Explicação profunda sobre Namespaces, Cgroups, Layered File System e Runtime.
- **O que é uma Imagem Docker.md**: Detalhes sobre a construção e estrutura de imagens.
- **Docker Compose.md**: Gerenciamento de stacks multi-container.
- **Boas Práticas e Otimização.md**: Multi-stage builds, cache de camadas e .dockerignore.
- **Redes no Docker.md**: Drivers de rede (Bridge, Host, Overlay) e comunicação DNS.
- **Segurança no Docker.md**: Usuário root, limites de recursos e imagens oficiais.
- **Orquestração com Kubernetes.md**: Transição do Docker para orquestradores.

### ☸️ Kubernetes (`/Kubernets`)
Uma coleção abrangente de guias e conceitos sobre orquestração de containers.
- **Kubernetes.md**: Visão geral e conceitos fundamentais do K8s.
- **como iniciar (Local).md**: Guia prático para Minikube, K3s e MicroK8s.
- **como iniciar (GKE).md** & **Gerenciamento de Nodes (GKE)**: Notas específicas sobre Google Kubernetes Engine.
- **Manifestos YAML e Persistência.md**: Exploração de recursos declarativos.
- **Helm - Gerenciador de Pacotes.md**: Automação de deployments.
- **Service Mesh - Istio.md** & **Gateway API**: Tópicos avançados de rede e comunicação.
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
