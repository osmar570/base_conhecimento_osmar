# Rancher: Gestão Centralizada de Clusters

O **Rancher** é uma plataforma completa de gerenciamento de [[Kubernetes]] que fornece uma interface gráfica (GUI) poderosa para administrar múltiplos clusters, independentemente de onde eles estejam rodando (GKE, AKS, EKS, Local ou Bare-metal).

---

## 1. O que é o Rancher?
Enquanto o `kubectl` é a ferramenta de linha de comando, o Rancher é o "Painel de Controle". Ele simplifica operações complexas como:
- Gerenciamento de múltiplos clusters em uma única tela.
- Controle de acesso (RBAC) centralizado.
- Provisionamento simplificado de novos clusters.
- Monitoramento e catálogo de aplicativos integrados.

---

## 2. Como Instalar o Rancher

### A. Para Testes e Estudos (Docker)
A forma mais rápida de subir o Rancher para conhecer a ferramenta é via Docker:

```bash
docker run -d --restart=unless-stopped \
  -p 80:80 -p 443:443 \
  --privileged \
  rancher/rancher:latest
```
Após rodar, acesse `https://localhost` no seu navegador.

### B. Para Produção (Via Helm)
Em ambientes profissionais, o Rancher deve ser instalado dentro de um cluster Kubernetes dedicado (geralmente um cluster pequeno de gerenciamento).

1. Adicione o repositório [[Helm - Gerenciador de Pacotes|Helm]]:
```bash
helm repo add rancher-stable https://releases.rancher.com/server-charts/stable
```

2. Instale o cert-manager (necessário para o SSL):
```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.yaml
```

3. Instale o Rancher:
```bash
helm install rancher rancher-stable/rancher \
  --namespace cattle-system \
  --set hostname=rancher.meudominio.com \
  --create-namespace
```

---

## 3. Conectando um Ambiente Kubernetes ao Rancher

Uma das funções mais comuns é o **"Import Cluster"**, onde você conecta um cluster existente (como o que você criou no [[como iniciar (GKE)]]) ao painel do Rancher.

### Passo a Passo para Importar:
1. No painel do Rancher, clique em **Clusters** -> **Import Existing**.
2. Dê um nome ao cluster.
3. O Rancher gerará um comando `kubectl apply`.
4. Copie esse comando e execute no seu terminal conectado ao cluster que deseja importar.

**O que acontece depois?**
O Rancher instalará um agente (Pod) dentro do seu cluster. Esse agente fará a comunicação segura com o painel do Rancher, permitindo que você gerencie [[Objetos Fundamentais|Pods, Deployments e Services]] visualmente.

---

## 4. Vantagens de usar o Rancher
1. **Catálogo de Apps:** Possui uma interface amigável para instalar [[Helm - Gerenciador de Pacotes|Charts do Helm]] com poucos cliques.
2. **Segurança:** Permite integrar com o Google Auth, GitHub ou AD para que sua equipe acesse o cluster com segurança.
3. **Visibilidade:** Facilita ver logs, abrir terminais dentro dos Pods e monitorar o consumo de recursos sem digitar comandos longos.

---
*Links relacionados:*
- [[Objetos Fundamentais]]
- [[Helm - Gerenciador de Pacotes]]
- [[Monitoramento de Nodes e Pods]]
