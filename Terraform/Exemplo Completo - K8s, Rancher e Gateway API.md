# Exemplo Prático: Infraestrutura K8s, Rancher e Gateway API

Este guia demonstra como arquitetar uma solução completa usando Terraform. Vamos provisionar duas máquinas Ubuntu, inicializar um cluster Kubernetes (K3s), instalar o Rancher via Helm e configurar a moderna **Gateway API** com **HTTPRoute**.

## 1. A Arquitetura

1.  **Infraestrutura (Terraform AWS):** Criação de 2 instâncias EC2 (Ubuntu 22.04).
2.  **Kubernetes (K3s):** O Nó 1 será o *Control Plane* e o Nó 2 será o *Worker*. Usamos scripts de `user_data` para instalar automaticamente na inicialização.
3.  **Gerenciamento (Rancher):** Instalado no cluster via *Terraform Helm Provider*.
4.  **Roteamento (Gateway API):** Substituição do antigo Ingress pelo novo padrão de `HTTPRoute`.

---

## 2. O Código Terraform (`main.tf`)

Neste exemplo simplificado, omitiremos a criação da VPC para focar nos nós e na configuração.

```hcl
# 1. Configuração do Provedor
provider "aws" {
  region = "us-east-1"
}

# 2. Encontrando a imagem do Ubuntu 22.04
data "aws_ami" "ubuntu" {
  most_recent = true
  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*"]
  }
  owners = ["099720109477"] # Canonical
}

# 3. Nó 1: K3s Control Plane (Server)
resource "aws_instance" "k8s_server" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t3.medium" # Rancher exige pelo menos 4GB de RAM
  
  # Script que roda quando a máquina liga
  user_data = <<-EOF
              #!/bin/bash
              curl -sfL https://get.k3s.io | sh -s - server \
                --cluster-init \
                --tls-san $(curl http://169.254.169.254/latest/meta-data/public-ipv4)
              
              # Extrai o token para o worker poder se juntar
              cat /var/lib/rancher/k3s/server/node-token > /tmp/node-token
              EOF

  tags = { Name = "k8s-control-plane" }
}

# 4. Nó 2: K3s Worker (Agent)
resource "aws_instance" "k8s_worker" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t3.medium"
  
  # O Worker precisa do IP do Server e do Token
  user_data = <<-EOF
              #!/bin/bash
              curl -sfL https://get.k3s.io | K3S_URL=https://${aws_instance.k8s_server.private_ip}:6443 \
              K3S_TOKEN="COLOQUE_O_TOKEN_AQUI_OU_USE_AWS_SECRETS" \
              sh -
              EOF

  tags = { Name = "k8s-worker" }
}
```

---

## 3. Instalando o Rancher via Terraform (Helm)

Depois que o cluster existe e o Terraform consegue ler o `kubeconfig`, podemos usar o provedor Helm do Terraform para instalar o Rancher automaticamente.

```hcl
provider "helm" {
  kubernetes {
    config_path = "~/.kube/config" # Apontando para o cluster recém criado
  }
}

resource "helm_release" "rancher" {
  name       = "rancher"
  repository = "https://releases.rancher.com/server-charts/latest"
  chart      = "rancher"
  namespace  = "cattle-system"
  create_namespace = true

  set {
    name  = "hostname"
    value = "rancher.meudominio.com"
  }
  
  set {
    name  = "replicas"
    value = "1" # Em produção, use 3
  }
}
```

---

## 4. Configurando a Rede: Gateway API e HTTPRoute

O Kubernetes tradicional usava o objeto `Ingress`. O novo padrão oficial é a **Gateway API**, que separa a infraestrutura da rede (Gateway) da lógica da aplicação (HTTPRoute).

Para usar isso no nosso cluster recém-criado, aplicamos os seguintes manifestos YAML (que também poderiam ser aplicados via Terraform usando o `kubernetes_manifest`):

### Passo A: Criar o Gateway (A porta de entrada)
Isso diz ao K8s para escutar na porta 80 e gerenciar o tráfego. Quem gerencia isso geralmente é o time de Infra/Plataforma.

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: meu-gateway-principal
  namespace: rede-infra
spec:
  gatewayClassName: nginx # Ou traefik, cilium, istio...
  listeners:
  - name: http
    protocol: HTTP
    port: 80
```

### Passo B: Criar o HTTPRoute (A Regra de Roteamento)
Isso é criado pelo desenvolvedor da aplicação. Ele "conecta" a aplicação ao Gateway existente.

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: rota-api-pagamentos
  namespace: app-pagamentos
spec:
  parentRefs:
  - name: meu-gateway-principal
    namespace: rede-infra
  hostnames:
  - "api.meudominio.com"
  rules:
  - matches:
    - path:
        type: PathPrefix
        value: /v1/pagamentos
    backendRefs:
    - name: servico-pagamentos
      port: 8080
```

### Vantagens dessa abordagem (Gateway API):
1.  **Separação de Papéis:** Infraestrutura cria o `Gateway` e Segurança/Devs criam o `HTTPRoute`. No modelo antigo (`Ingress`), tudo ficava misturado em um arquivo só.
2.  **Roteamento Avançado:** O `HTTPRoute` suporta nativamente testes Canary (dividir tráfego por peso, ex: 90% / 10%), manipulação de Headers de HTTP e espelhamento de tráfego, coisas que no Ingress antigo exigiam gambiarras com *annotations*.

---
**Links Relacionados:**
- [[Terraform]]
- [[como iniciar (Local)]] (Para conceitos de K3s)
- [[Gateway API e HTTPRoute]]
- [[Kubernetes]]
- [[Docker]]
