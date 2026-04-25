# ConfigMaps e Secrets

No [[Kubernetes]], uma das melhores práticas é a separação entre o código da aplicação e sua configuração. Isso permite que a mesma imagem de container rode em diferentes ambientes (Dev, Homolog, Prod) apenas alterando os objetos de configuração, sem precisar editar o [[Manifestos YAML e Persistência|YAML do Deployment]].

---

## 1. ConfigMaps
O **ConfigMap** é usado para armazenar dados não confidenciais em pares chave-valor.

*   **Uso comum:** Variáveis de ambiente, arquivos de configuração (como um `nginx.conf` ou `settings.json`), ou argumentos de linha de comando.
*   **YAML de exemplo:**
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_COLOR: "blue"
  LOG_LEVEL: "debug"
  API_URL: "https://api.meusite.com"
```

---

## 2. Secrets
O **Secret** é semelhante ao ConfigMap, mas projetado especificamente para armazenar dados sensíveis.

*   **Uso comum:** Senhas, chaves de API, tokens de acesso e certificados SSH.
*   **Segurança:** Por padrão, os dados em um Secret são armazenados em **Base64**. No entanto, para segurança real, recomenda-se usar criptografia em repouso (etcd) ou ferramentas externas (como HashiCorp Vault ou Google Secret Manager no [[como iniciar (GKE)]]).
*   **YAML de exemplo:**
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secrets
type: Opaque
data:
  DB_PASSWORD: dXNlcjpwYXNzd29yZA== # "user:password" em base64
```
> **Dica:** Para gerar o base64 no terminal Linux: `echo -n "minhasenha" | base64`

---

## 3. Como usar em um Deployment
Você pode injetar esses dados nos seus [[Objetos Fundamentais|Pods]] de duas formas principais:

### Como Variáveis de Ambiente
```yaml
spec:
  containers:
  - name: minha-app
    image: minha-imagem:latest
    env:
      - name: DB_PASS
        valueFrom:
          secretKeyRef:
            name: app-secrets
            key: DB_PASSWORD
      - name: APP_MODE
        valueFrom:
          configMapKeyRef:
            name: app-config
            key: APP_COLOR
```

### Como Arquivos Montados (Volumes)
Útil para arquivos de configuração inteiros.
```yaml
spec:
  containers:
    - name: nginx
      image: nginx
      volumeMounts:
      - name: config-volume
        mountPath: /etc/config
  volumes:
    - name: config-volume
      configMap:
        name: app-config
```

---

## 4. ConfigMaps Imutáveis
A partir do Kubernetes 1.19, é possível marcar ConfigMaps e Secrets como **imutáveis**.
*   **Vantagem:** Reduz a carga no `kube-apiserver` (o Kubelet para de monitorar mudanças) e garante que as configurações não sejam alteradas acidentalmente.
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: static-config
data:
  config: "valor"
immutable: true
```

---

## 5. Hot Reload: Mounting vs Env Vars
A forma como você consome o ConfigMap afeta como as atualizações são propagadas:

1.  **Variáveis de Ambiente:** O valor é injetado no momento da criação do Pod. Se o ConfigMap mudar, o Pod **não** recebe o novo valor até ser reiniciado.
2.  **Volumes (Mounting):** O Kubelet atualiza o arquivo montado periodicamente. Se a aplicação for capaz de monitorar mudanças no arquivo (ex: `fsnotify`), ela pode fazer o **Hot Reload** sem reiniciar o Pod.

---

## 🛡️ Boas Práticas e Segurança

1.  **Não versionar Secrets no Git:** Utilize ferramentas como **Sealed Secrets**, **Sops** ou integre com **External Secrets Operator** para buscar dados de um Vault externo (GCP Secret Manager, Azure Key Vault).
2.  **Princípio do Menor Privilégio:** Use [[RBAC e Governança|RBAC]] para limitar quem pode ler os Secrets em cada Namespace.
3.  **Tamanho Limite:** O tamanho máximo de um ConfigMap ou Secret é de **1MB**. Para arquivos maiores, utilize volumes externos ou Persistent Volumes.
4.  **Prefixos nas Chaves:** Use nomes claros nas chaves (`DATABASE_URL` em vez de apenas `URL`) para evitar colisões quando injetadas como variáveis de ambiente.

---

## Comandos úteis:
```bash
# Criar rapidamente via linha de comando
kubectl create configmap minha-config --from-literal=chave=valor

# Visualizar o conteúdo (Secrets precisam de decodificação)
kubectl get configmap app-config -o yaml
kubectl get secret app-secrets -o jsonpath='{.data.DB_PASSWORD}' | base64 --decode
```
