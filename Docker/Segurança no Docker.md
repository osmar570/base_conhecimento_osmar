# Segurança no Docker

Segurança em containers é baseada no princípio do **Privilégio Mínimo**. Um container nunca deve ter mais acesso do que o estritamente necessário para funcionar.

## 1. O Perigo do Usuário Root

Por padrão, muitos containers rodam como `root`. Se um invasor explorar uma falha na sua aplicação, ele terá privilégios de root dentro do container e, possivelmente, tentará um "container breakout" para o host.

**✅ Solução:** Use a instrução `USER` no seu Dockerfile.
```dockerfile
RUN groupadd -r appgroup && useradd -r -g appgroup appuser
USER appuser
```

## 2. Limitação de Recursos (Prevenção de DoS)

Um único container bugado ou malicioso pode consumir toda a CPU/RAM do servidor, derrubando todos os outros serviços.

*   **Limite de Memória:** `--memory="512m"`
*   **Limite de CPU:** `--cpus="1.5"`

## 3. Sistema de Arquivos Read-Only

Sempre que possível, rode seu container com o sistema de arquivos apenas para leitura. Isso impede que um invasor baixe scripts maliciosos ou altere arquivos de configuração.

*   `docker run --read-only ...`
*   Combine com volumes específicos para as pastas que **realmente** precisam de escrita (ex: `/tmp`, `/var/logs`).

## 4. Escaneamento de Imagens

Imagens no Docker Hub podem conter vulnerabilidades conhecidas (CVEs).
*   Use ferramentas como **Docker Scout**, **Trivy** ou **Snyk** para escanear suas imagens antes de subir para produção.
*   Mantenha suas imagens base atualizadas.

## 5. Dicas Rápidas de Segurança

1.  **Segredos:** Nunca use `ENV` para senhas ou chaves de API. Use **Docker Secrets** ou **Volumes** para montar arquivos de configuração sensíveis.
2.  **Imagens Oficiais:** Prefira sempre imagens "Official Image" ou de editores verificados no Docker Hub.
3.  **Privileged Mode:** **NUNCA** use `--privileged` em produção, a menos que você saiba exatamente o que está fazendo (isso dá acesso quase total ao hardware do host).

---
**Links Relacionados:**
- [[Boas Práticas e Otimização]]
- [[O que são Containers (Detalhes Técnicos)]]
- [[Docker]]