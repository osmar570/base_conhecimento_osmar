# Shell Scripting e Automação (.sh)

Um **Shell Script** é um arquivo de texto que contém uma sequência de comandos que o sistema operacional executa em ordem. É a forma mais pura e poderosa de automação no Linux.

---

## 1. Anatomia de um Script

Todo script Linux deve começar com a "Shebang" (`#!`), que diz ao sistema qual interpretador usar.

```bash
#!/bin/bash

# Isso é um comentário
NOME="Osmar"
echo "Olá $NOME, iniciando automação..."
```

### Como executar:
1.  **Dar permissão de execução:** `chmod +x meu_script.sh`
2.  **Rodar:** `./meu_script.sh`

---

## 2. Exemplos Práticos para o Dia a Dia

Aqui estão tarefas comuns que você pode automatizar:

### A. Script de Backup Simples
Compacta uma pasta e salva em um diretório de backup com a data atual.
```bash
#!/bin/bash
DATA=$(date +%Y-%m-%d)
ORIGEM="/home/usuario/meu_projeto"
DESTINO="/home/usuario/backups"

mkdir -p $DESTINO
tar -czf $DESTINO/backup-$DATA.tar.gz $ORIGEM
echo "Backup concluído em $DESTINO"
```

### B. Manutenção do Docker (Limpeza)
Automatiza a limpeza de lixo que o Docker acumula.
```bash
#!/bin/bash
echo "Iniciando limpeza do Docker..."
docker container prune -f
docker image prune -f
docker volume prune -f
echo "Sistema Docker limpo!"
```

### C. Verificador de Saúde (Health Check)
Verifica se um site ou serviço está online e avisa se estiver fora do ar.
```bash
#!/bin/bash
URL="https://google.com"
if curl -s --head $URL | grep "200 OK" > /dev/null
then
    echo "O site $URL está online!"
else
    echo "ALERTA: $URL está fora do ar!"
fi
```

---

## 3. Agendamento com Crontab

Não adianta ter um script de backup se você tiver que rodar ele manualmente. Para isso usamos o **Cron**.

*   **Comando:** `crontab -e`
*   **Exemplo de regra:**
    `0 2 * * * /home/usuario/scripts/backup.sh`
    *(Isso executará o script todos os dias às 2 horas da manhã).*

---

## 4. Por que automatizar com Shell Script?

1.  **Repetibilidade:** Você garante que a tarefa será feita exatamente da mesma forma sempre.
2.  **Velocidade:** Executar um script de instalação de 50 pacotes é muito mais rápido que digitar um por um.
3.  **Documentação Viva:** O script serve como documento de como aquela tarefa deve ser executada.
4.  **Integração:** Scripts são a "cola" que une diferentes ferramentas (Docker, Git, AWS CLI, etc.).

---
**Links Relacionados:**
- [[Linux]]
- [[Comandos Essenciais de Terminal]]
- [[Docker Cheat Sheet]] (Muitos scripts automatizam comandos Docker)
