# Troubleshooting no Docker

Depurar Docker é, em grande parte, entender por que um processo isolado não está se comportando como esperado no sistema host.

## 1. Analisando Exit Codes

Quando um container morre, o Docker retorna um código que indica a causa:

| Código | Significado | Causa Provável |
| :--- | :--- | :--- |
| **137** | **SIGKILL** | O container foi morto pelo SO, geralmente por falta de memória (OOM). |
| **127** | **Command not found** | O binário especificado no `CMD` ou `ENTRYPOINT` não existe na imagem. |
| **139** | **Segmentation Fault** | A aplicação tentou acessar memória que não deveria (bug no código). |
| **1** | **Application Error** | Erro genérico de execução da aplicação. |

## 2. Inspeção Profunda com `docker inspect`

O comando `inspect` retorna um JSON gigante com tudo sobre o container. Use `grep` ou format para filtrar:

*   **Verificar o IP do container:**
    `docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container_id>`
*   **Verificar as variáveis de ambiente carregadas:**
    `docker inspect <container_id> | grep -A 10 "Env"`

## 3. Depuração de Recursos

Se o seu computador estiver lento ou o container estiver travando:
*   **`docker stats`**: Monitoramento em tempo real de CPU, Memória e I/O de rede de todos os containers ativos.
*   **`docker top <container_id>`**: Lista os processos rodando **dentro** daquele container (visão do SO).

## 4. Problemas de Rede e Conectividade

Se um container não consegue falar com outro:
1.  **Rede correta?** Verifique se estão na mesma rede: `docker network inspect <nome_da_rede>`.
2.  **DNS Interno:** Tente dar um `ping` no nome do outro container de dentro de um shell interativo.
3.  **Portas:** O comando `docker port <container_id>` mostra exatamente quais portas estão mapeadas para o host.

## 5. Limpeza e "Reset" do Ambiente

Muitas vezes, problemas bizarros são causados por falta de espaço em disco ou camadas corrompidas.
*   **`docker system prune`**: Remove containers parados, redes não usadas e imagens pendentes (dangling).
*   **`docker volume prune`**: Remove volumes não utilizados (cuidado, deleta dados!).
*   **Verificar espaço em disco do Docker:** `docker system df`.

## 6. O Container não inicia (Erro de Entrypoint)

Se o container fecha instantaneamente e não gera logs:
*   Tente rodar sobrescrevendo o entrypoint para um shell:
    `docker run -it --entrypoint /bin/sh <imagem>`
    Isso permite que você explore o sistema de arquivos e verifique se as dependências estão lá.

---
**Links Relacionados:**
- [[Docker]]
- [[Redes no Docker]]
- [[Segurança no Docker]]
