# Helm: O Gerenciador de Pacotes do [[Kubernetes]]

Se o Kubernetes é o sistema operacional do seu cluster, o **Helm** é o seu `apt`, `yum` ou `npm`. Ele permite empacotar, configurar e implantar aplicações complexas com um único comando.

---

## 1. Por que usar o Helm?
Escrever [[Manifestos YAML e Persistência|arquivos YAML]] manualmente para cada aplicação pode ser repetitivo e propenso a erros. O Helm resolve isso através de:

*   **Templates:** Em vez de valores fixos, você usa variáveis. O mesmo pacote (Chart) pode ser usado para Dev, Homolog e Prod apenas mudando um arquivo de valores.
*   **Gerenciamento de Versões:** O Helm mantém um histórico de tudo o que você instalou. Se uma atualização der errado, você pode fazer um **Rollback** instantâneo.
*   **Reuso:** Você pode usar pacotes prontos da comunidade (como Bancos de Dados, [[Ingress e Ingress Controllers|Ingress Controllers]], ferramentas de monitoramento) sem precisar escrever o código do zero.

---

## 2. Conceitos Principais

-   **Chart:** É o pacote em si. Um conjunto de arquivos YAML organizados em uma pasta que descrevem um conjunto de recursos do Kubernetes.
-   **Release:** É uma instância de um Chart rodando no cluster. Você pode instalar o mesmo Chart (ex: MySQL) várias vezes, gerando releases diferentes (ex: `mysql-vendas`, `mysql-clientes`).
-   **Repository:** Um servidor onde os Charts são armazenados e compartilhados (semelhante ao Docker Hub ou npm registry).

---

## 3. Comandos Essenciais

### Instalação e Repositórios
```bash
# Adicionar um repositório (ex: Bitnami, que tem muitos apps prontos)
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
```

### Instalando uma Aplicação
```bash
# Instala o WordPress com o nome "meu-blog"
helm install meu-blog bitnami/wordpress
```

### Gerenciando Releases
```bash
# Lista tudo o que foi instalado via Helm
helm list

# Atualiza uma aplicação após mudar configurações
helm upgrade meu-blog bitnami/wordpress

# Volta para a versão anterior em caso de erro
helm rollback meu-blog 1

# Remove a aplicação e todos os seus recursos do cluster
helm uninstall meu-blog
```

---

## 4. O Arquivo `values.yaml`
Este é o coração do Helm. Nele você define as customizações. Por exemplo, para mudar a senha do banco ou o número de réplicas de um Pod:

```yaml
# exemplo de values.yaml simplificado
replicaCount: 3
service:
  type: LoadBalancer
  port: 80
```
Para aplicar: `helm install meu-app ./meu-chart -f values.yaml`

---

## 5. Exemplo Prático: Instalando o Nginx Ingress
Como vimos em [[Ingress e Ingress Controllers]], instalar o controller manualmente pode ser complexo. Com Helm é apenas um comando:

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm install meu-ingress ingress-nginx/ingress-nginx
```

---

## Resumo
O Helm transforma o gerenciamento do Kubernetes de "editar centenas de linhas de YAML" para "gerenciar pacotes e versões", tornando o processo de CI/CD muito mais seguro e padronizado.
