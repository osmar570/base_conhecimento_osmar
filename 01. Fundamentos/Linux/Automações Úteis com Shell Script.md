# Automações Úteis com Shell Script

Esta nota contém uma lista de scripts prontos para facilitar o dia a dia de um desenvolvedor ou administrador de sistemas.

---

## 1. Sincronização Automática do Vault (Git)
Ideal para manter suas notas do Obsidian sempre salvas no GitHub sem precisar digitar os comandos toda hora.
```bash
#!/bin/bash
echo "Iniciando sincronização do Vault..."
git add .
git commit -m "Auto-commit: $(date +'%Y-%m-%d %H:%M:%S')"
git push origin main
echo "Vault sincronizado com sucesso!"
```

---

## 2. Atualizador Geral de Repositórios
Entra em todas as pastas de um diretório e roda `git pull` em cada uma delas.
```bash
#!/bin/bash
# Pasta onde ficam seus projetos
BASE_DIR="$HOME/projetos"

for d in $BASE_DIR/*/ ; do
    echo "Atualizando: $d"
    cd "$d" && git pull
done
```

---

## 3. Limpeza de Logs e Arquivos Temporários
Libera espaço em disco removendo arquivos que se acumulam com o tempo.
```bash
#!/bin/bash
echo "Limpando arquivos temporários e logs antigos..."
sudo rm -rf /tmp/*
sudo find /var/log -type f -name "*.log" -exec truncate -s 0 {} +
echo "Espaço em disco após limpeza:"
df -h | grep '^/'
```

---

## 4. Backup de Banco de Dados (PostgreSQL)
Extrai um dump do banco, compacta e mantém apenas os últimos 7 dias de backup.
```bash
#!/bin/bash
DB_NAME="meu_banco"
BACKUP_DIR="$HOME/backups/db"
DATA=$(date +%Y%m%d)

mkdir -p $BACKUP_DIR
pg_dump $DB_NAME | gzip > $BACKUP_DIR/db_backup_$DATA.sql.gz

# Deleta backups com mais de 7 dias
find $BACKUP_DIR -type f -mtime +7 -name "*.gz" -delete
echo "Backup do banco $DB_NAME realizado!"
```

---

## 5. Localizador de Arquivos Pesados
Encontra os 10 maiores arquivos do seu sistema para você saber o que está consumindo o disco.
```bash
#!/bin/bash
echo "Os 10 maiores arquivos em /home:"
sudo du -ah /home | sort -rh | head -n 10
```

---

## 6. Verificador de Portas Abertas
Útil para segurança e para descobrir qual programa está travando uma porta que você precisa usar.
```bash
#!/bin/bash
echo "Serviços ouvindo em portas de rede:"
sudo netstat -tulpn | grep LISTEN
```

---

## 7. Criador de Estrutura de Projeto (Boilerplate)
Cria rapidamente as pastas padrão para um novo projeto seguindo a sua estrutura preferida.
```bash
#!/bin/bash
mkdir -p src/{domain,application,infrastructure,webapi}
touch src/domain/entities.txt README.md .gitignore
echo "Estrutura Clean Architecture criada!"
```

---

## 💡 Como organizar seus scripts
Uma boa prática é criar uma pasta `~/scripts`, colocar todos os arquivos lá e adicionar essa pasta ao seu **PATH** no arquivo `~/.bashrc`:
`export PATH="$PATH:$HOME/scripts"`

Assim, você pode rodar qualquer um desses scripts apenas digitando o nome dele em qualquer lugar do terminal.

---
**Links Relacionados:**
- [[Shell Scripting e Automação]]
- [[Linux]]
- [[Clean Architecture]] (Para o script de boilerplate)
