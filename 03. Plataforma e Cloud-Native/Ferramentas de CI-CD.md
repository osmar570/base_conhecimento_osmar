# Ferramentas de CI/CD

CI/CD é a espinha dorsal da cultura DevOps. Ela permite que as equipes entreguem alterações de código com mais frequência e confiabilidade através da automação de testes, builds e deploys.

---

## 🔄 Conceitos Fundamentais

### 1. CI - Continuous Integration (Integração Contínua)
Prática de integrar mudanças de código no repositório principal várias vezes ao dia.
- **Objetivo:** Detectar erros rapidamente através de builds e testes automáticos.
- **Etapas comuns:** Linting, Testes Unitários e Build da imagem Docker.

### 2. CD - Continuous Delivery vs. Deployment
- **Continuous Delivery:** O código está sempre pronto para ser deployado, mas a entrada em produção exige uma aprovação manual.
- **Continuous Deployment:** Toda alteração que passa nos testes é deployada automaticamente em produção.

---

## 🛠️ Principais Ferramentas

### 1. GitHub Actions
Nativo do GitHub, utiliza arquivos YAML para definir os fluxos.
- **Vantagem:** Integração total com o repositório e uma enorme comunidade de ações prontas.

### 2. GitLab CI/CD
Focado em pipelines robustos e integrados à plataforma GitLab.
- **Vantagem:** Excelente suporte a Auto DevOps e gerenciamento de containers.

### 3. Jenkins
A ferramenta de automação "clássica".
- **Vantagem:** Altamente customizável através de plugins, mas exige manutenção de servidor própria.

### 4. ArgoCD (GitOps)
Focado especificamente em Kubernetes.
- **Conceito:** Sincroniza o estado do cluster com o que está definido no Git.
- [[03. Plataforma e Cloud-Native/Kubernetes/GitOps e CD Moderno|Saiba mais sobre GitOps]]

---

## 🚀 Exemplo Prático: GitHub Actions (.yml)

```yaml
name: CI/CD Pipeline
on: [push]
jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup .NET
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: '8.0.x'
      - name: Install dependencies
        run: dotnet restore
      - name: Build
        run: dotnet build --no-restore
      - name: Test
        run: dotnet test --no-build --verbosity normal
```

---
**Links Relacionados:**
- [[02. Engenharia de Software/Estratégia de Testes|Estratégia de Testes]] (O que o pipeline executa)
- [[03. Plataforma e Cloud-Native/Docker/Docker|Docker]] (Unidade de entrega do CI/CD)
- [[05. Trilhas de Estudos/DevOps|Trilha de DevOps]]
