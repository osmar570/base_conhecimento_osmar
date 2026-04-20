# 🧠 Base de Conhecimento: Engenharia de Software & Cloud-Native

Este repositório é um **Vault do Obsidian** de nível profissional, focado em documentação técnica, padrões de arquitetura e notas de estudo sobre o ecossistema moderno de desenvolvimento e infraestrutura.

---

## 📂 Organização da Base

O conhecimento está estruturado em pilares fundamentais, cada um com seu guia de entrada centralizado.

### 🐳 Docker (`/Docker`)
Conceitos de conteinerização e isolamento de processos.
- **Introdução ao Docker e Conteinerização.md**: O ponto de partida com trilha de aprendizagem.
- **O que são Containers (Detalhes Técnicos).md**: Kernel Linux, Namespaces e Cgroups.
- **O que é uma Imagem Docker.md**: Dockerfiles e estrutura de camadas.
- **Docker Compose.md**: Orquestração local de múltiplos serviços.
- **Persistência de Dados (Volumes).md**: Diferença entre Volumes e Bind Mounts.
- **Redes no Docker.md**: Drivers de rede e DNS interno.
- **Boas Práticas e Otimização.md**: Multi-stage builds e cache de camadas.
- **Segurança no Docker.md**: Privilégio mínimo e escaneamento de vulnerabilidades.
- **Troubleshooting no Docker.md**: Diagnóstico de erros e exit codes.
- **Docker Cheat Sheet.md**: Guia de referência rápida para comandos.

### ☸️ Kubernetes (`/Kubernetes`)
Orquestração de containers em escala industrial.
- **Kubernetes.md**: Guia mestre de conceitos e arquitetura.
- **Objetos Fundamentais.md**: Pods, Services, Deployments e ConfigMaps.
- **Troubleshooting no Kubernetes.md**: Fluxo de depuração e estados de erro.
- **RBAC e Governança.md**: Segurança, Roles e ServiceAccounts.
- **GitOps e CD Moderno.md**: Reconciliação automática (ArgoCD/Flux).
- **Guia Prático de GitOps.md**: Instalação e monitoramento do Argo CD.
- **Estratégias de Deployment.md**: Rolling Update, Blue/Green e Canary.
- **Gateway API e HTTPRoute.md**: A evolução moderna do roteamento de rede.
- **Helm - Gerenciador de Pacotes.md**: Automação de manifestos.
- **Monitoramento e Autoscaling.md**: Observabilidade e escalabilidade horizontal.
- **como iniciar (Local).md**: Guia para Minikube, K3s e MicroK8s.
- **como iniciar (GKE).md**: Guia para Google Kubernetes Engine.

### 🏗️ Terraform (`/Terraform`)
Infraestrutura como Código (IaC) e automação de nuvem.
- **Terraform.md**: Fundamentos, Providers e o arquivo de State.
- **Arquitetura e Comandos do Terraform.md**: O ciclo de vida (Init, Plan, Apply).
- **Backend Remoto e State Locking.md**: Colaboração segura em equipe.
- **Lógica Avançada e Ciclo de Vida.md**: Meta-arguments (`for_each`, `count`).
- **Workspaces e Ambientes.md**: Estratégias para Dev, Staging e Produção.
- **Terraform Import.md**: Assumindo o controle de infraestrutura existente.
- **Segurança e Gestão de Segredos.md**: Integração com Secret Managers.
- **Ferramentas do Ecossistema.md**: Linting (tflint) e Segurança (tfsec).
- **Exemplo Completo - K8s, Rancher e Gateway API.md**: Arquitetura real provisionada via IaC.
- **Monitoramento e Autoscaling**: Práticas de observabilidade e escalabilidade.

### 📐 Engenharia de Software (`/Engenharia de Software`)
Conceitos transversais ao desenvolvimento e aspectos legais.
- **Engenharia de Software.md**: Índice de padrões e trilha de aprendizagem.
- **Licenças de Software.md**: MIT, Apache, GPL e modelos de distribuição.
- **Versão Semântica (SemVer).md**: O padrão MAJOR.MINOR.PATCH e sua importância na estabilidade do software.

### 🏛️ Clean Architecture (`/Clean Architecture`)
Padrões de design para software sustentável e testável.
- **Clean Architecture.md**: O arquivo mestre e a Regra da Dependência.
- **Regra da Dependência e DIP.md**: Inversão de dependência na prática.
- **Detalhamento das Camadas (Entities e Use Cases).md**: O núcleo do negócio.
- **Interface Adapters (Controllers e Gateways).md**: Tradução entre camadas.
- **Diferença entre Clean vs Hexagonal.md**: Comparativo técnico de padrões.
- **Exemplo Prático CSharp.md**: Estrutura de Solution .NET e Value Objects vs DTOs.

### 🤖 LLMs & Inteligência Artificial (`/LLMs`)
O estado da arte em IA Generativa e Agentes.
- **LLMs.md**: Índice de conceitos e trilha de aprendizagem.
- **Fundamentos de GenAI.md**: Transformers e Mecanismo de Atenção.
- **Prompt Engineering Avançado.md**: Técnicas de raciocínio e frameworks.
- **RAG (Retrieval-Augmented Generation).md**: Conectando LLMs a dados privados.
- **Guia Prático de Implementação de RAG.md**: Ferramentas e código Python.
- **Agentes e Ferramentas.md**: LLMs como orquestradores (Ciclo ReAct).
- **Arquitetura de Multiagentes.md**: Equipes de IAs colaborativas (CrewAI).
- **Hospedando IAs Locais com Docker.md**: Ollama e Open WebUI.
- **Fine-tuning de LLMs.md**: Ajuste específico com PEFT e LoRA.
- **Arquitetura Modular para IA.md**: Criando aplicações de IA desacopladas.

### 📜 Git e Boas Práticas (`/Git`)
Padrões de colaboração e versionamento de código.
- **Git.md**: Índice de padrões, estratégias de branch e hooks.
- **Git Cheat Sheet.md**: Guia de referência rápida para comandos de commit, branch e remoto.
- **Conventional Commits e Commit Lint.md**: Padronização de mensagens de commit para histórico rastreável.

### 🐧 Linux (`/Linux`)
A base de toda a infraestrutura moderna.
- **Linux.md**: Visão geral e vantagens do Kernel.
- **Arquitetura de Diretórios.md**: O padrão FHS (/etc, /var, /home).
- **Comandos Essenciais de Terminal.md**: Navegação e administração.
- **SSH e Acesso Remoto.md**: Segurança e gestão de múltiplos servidores.
- **Sistema de Permissões.md**: Gestão de rwx, usuários e grupos.
- **Gerenciamento de Pacotes.md**: APT, DNF, Pacman e pacotes universais.
- **Shell Scripting e Automação.md**: Criação de scripts .sh e Crontab.
- **Automações Úteis com Shell Script.md**: Coleção de scripts prontos.
- **Processamento de Texto (Grep, Sed, Awk).md**: Manipulação avançada de texto.
- **Processos e Monitoramento.md**: Gestão de recursos e PID.
- **Redes no Linux.md**: Diagnóstico e Firewall (UFW/IPTables).
- **Troubleshooting no Linux.md**: Diagnóstico de logs, hardware, disco e falhas de boot.

---

## 🚀 Como Utilizar

Este repositório foi projetado para ser visualizado no **Obsidian**, aproveitando os links internos para navegação fluida.

1.  **Início Rápido**: Comece pelos arquivos de índice em cada pasta (ex: `Linux.md` ou `Docker.md`).
2.  **Interconexão**: Fique atento aos **WikiLinks** `[[Link]]`, eles conectam conceitos entre diferentes tecnologias.
3.  **Scripts**: Muitos guias contêm exemplos de código e scripts prontos para uso imediato em seu terminal.

## 🛠️ Convenções
- **Idioma:** Notas escritas em **Português (PT-BR)**.
- **Sintaxe:** Markdown padrão + extensões Obsidian.
- **Índice por Assunto:** Cada pasta possui um arquivo principal com o nome da pasta que atua como ponto de entrada.
