# Segurança em Contêineres

Em ambientes Cloud-Native, a segurança do contêiner é uma camada crítica que vai além da segurança da aplicação.

## 🛡️ Pilares da Segurança
1. **Segurança da Imagem**:
    - Usar imagens base leves e oficiais (ex: Alpine, Distroless).
    - **Scanning**: Detectar vulnerabilidades em bibliotecas do SO e dependências (ferramentas: Trivy, Grype, Snyk).
    - **Assinatura de Imagem**: Garantir a procedência da imagem (ex: Docker Content Trust, Cosign).

2. **Segurança em Runtime**:
    - **Privileged Mode**: Nunca rodar contêineres como `--privileged`.
    - **User ID**: Evitar rodar processos como `root` dentro do contêiner (User Namespaces).
    - **Read-Only Root Filesystem**: Impedir que atacantes escrevam binários maliciosos no disco.

3. **Isolamento de Recursos**:
    - Definir `limits` e `requests` de CPU e Memória para evitar ataques de Negação de Serviço (DoS) entre contêineres vizinhos.
    - **Capabilities**: Remover capabilities do Kernel desnecessárias (ex: `cap_drop: [ALL]`).

## 🛠️ Ferramentas de Auditoria
* **Trivy**: Scanner de vulnerabilidades e misconfigurations.
* **Falco**: Detecção de intrusão em tempo de execução para Kubernetes.
* **Docker Bench for Security**: Script que verifica se o Docker está configurado conforme as boas práticas do CIS.
