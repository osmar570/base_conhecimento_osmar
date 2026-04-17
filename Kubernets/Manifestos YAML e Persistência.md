# Manifestos YAML e Persistência de Dados

No [[Kubernetes]], quase tudo é definido através de arquivos **YAML**. Esses arquivos descrevem o "estado desejado" do seu cluster, e o Kubernetes trabalha para garantir que esse estado seja mantido (conceito explicado em [[Objetos Fundamentais]]).

## Estrutura Básica de um YAML
Todo manifesto Kubernetes possui quatro campos obrigatórios:
1.  **apiVersion:** Versão da API do Kubernetes.
2.  **kind:** O tipo de objeto (Pod, Deployment, Service, etc).
3.  **metadata:** Dados que ajudam a identificar o objeto (nome, labels, namespace).
4.  **spec:** A especificação técnica do que o objeto deve fazer.

---

## Persistência: PV e PVC
Como vimos em [[Objetos Fundamentais]], os Pods são efêmeros. Se um container de banco de dados cair, os dados dentro dele sumirão. Para resolver isso, usamos:

*   **Persistent Volume (PV):** Um pedaço de armazenamento real (disco na nuvem ou na rede local) configurado pelo administrador.
*   **Persistent Volume Claim (PVC):** Uma "requisição" de um usuário para usar um pedaço desse PV.

---

## Exemplo Prático: Nginx com Armazenamento Persistente

Abaixo, um exemplo completo de como subir um Nginx que salva seus logs ou arquivos de forma permanente.

### 1. Criando o Armazenamento (PV e PVC)
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nginx-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data" # Usado em ambientes como o [[como iniciar (Local)]]
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nginx-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

### 2. O Deployment do Nginx usando o PVC
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
        volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: storage-nginx
      volumes:
      - name: storage-nginx
        persistentVolumeClaim:
          claimName: nginx-pvc
```

---

## Como subir os objetos no Cluster
Após salvar o conteúdo acima em um arquivo chamado `meu-nginx.yaml`, utilize o comando principal do `kubectl`:

```bash
# Aplica a configuração no cluster
kubectl apply -f meu-nginx.yaml

# Verifica se o PV e o PVC foram criados e vinculados (Bound)
kubectl get pv,pvc

# Verifica se o Deployment subiu corretamente
kubectl get deployments
```

### Dicas Importantes:
- Se você estiver no [[como iniciar (GKE)]], o GKE possui **StorageClasses** que criam o PV automaticamente quando você define apenas o PVC.
- Use sempre o `kubectl apply` em vez de `kubectl create`, pois o `apply` permite atualizar o objeto futuramente apenas editando o YAML e rodando o comando novamente.
