# Como Iniciar [[Kubernetes]] em Rede Local

Para rodar o Kubernetes localmente sem depender de provedores de nuvem, existem várias ferramentas que simulam um cluster de forma eficiente.

## 1. Minikube (Ideal para Desenvolvimento)
O Minikube cria um cluster de nó único dentro de uma máquina virtual ou container (Docker).

### Instalação (Linux)
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

### Inicialização
```bash
# Inicia o cluster usando o driver do Docker (recomendado)
minikube start --driver=docker

# Verifica o status
minikube status
```

---

## 2. K3s (Leve e para Servidores Locais)
Desenvolvido pela Rancher, o K3s é uma distribuição extremamente leve, ideal para rodar em servidores locais, Raspberry Pi ou ambientes com poucos recursos.

### Instalação Rápida
```bash
curl -sfL https://get.k3s.io | sh -
# O arquivo de configuração ficará em /etc/rancher/k3s/k3s.yaml
```

### Verificação
```bash
sudo kubectl get nodes
```

---

## 3. MicroK8s (Nativo para Ubuntu/Linux)
Se você usa distribuições baseadas em Debian/Ubuntu, o MicroK8s é uma excelente opção via Snap.

### Instalação
```bash
sudo snap install microk8s --classic
sudo usermod -a -G microk8s $USER
# Reinicie a sessão para aplicar as permissões
```

### Inicialização e Comandos
```bash
microk8s status --wait-ready
microk8s kubectl get nodes
```

---

## Ferramenta Essencial: Kubectl
Independente da escolha acima, você precisará do `kubectl` para gerenciar o cluster:

```bash
sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates curl
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```

## Resumo de Escolha
- **Minikube:** Melhor para aprender e testar manifestos rapidamente no seu PC.
- **K3s:** Melhor para montar um "Home Lab" com computadores antigos ou servidores dedicados na rede.
- **MicroK8s:** Melhor integração se você já utiliza o ecossistema Ubuntu/Canonical.
