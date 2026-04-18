# Processamento de Texto (Grep, Sed, Awk)

No Linux, "tudo é texto". Dominar estas três ferramentas permite que você filtre, edite e transforme dados diretamente no terminal, sendo essencial para análise de logs e automação.

---

## 1. Grep (O Localizador)
O `grep` busca padrões dentro de arquivos ou da saída de outros comandos.

*   **Busca simples:** `grep "erro" log_sistema.txt`
*   **Ignorar maiúsculas/minúsculas:** `grep -i "usuario" arquivo.txt`
*   **Recursivo (em pastas):** `grep -r "conexao_recusada" /var/log/`
*   **Inverter busca (o que NÃO tem a palavra):** `grep -v "debug" log.txt`
*   **Regex (Expressões Regulares):** `grep -E "[0-9]{1,3}\.[0-9]{1,3}"` (Busca padrões de IP).

---

## 2. Sed (O Editor de Fluxo)
O `sed` é usado para transformar ou filtrar texto. Ele edita o arquivo "no ar" ou cria uma versão modificada sem precisar abrir um editor como o Vim.

*   **Substituir palavra (S de Substitute):** 
    `sed 's/antigo/novo/g' arquivo.txt` (O `g` troca todas as ocorrências na linha).
*   **Editar o arquivo original diretamente:** 
    `sed -i 's/localhost/127.0.0.1/g' config.env`
*   **Deletar linhas que contenham um padrão:** 
    `sed '/debug/d' log.txt`
*   **Trocar apenas em uma linha específica:** 
    `sed '5s/desligado/ligado/' arquivo.txt` (Troca apenas na linha 5).

---

## 3. Awk (O Processador de Colunas)
O `awk` trata o arquivo como se fosse uma tabela (banco de dados). Ele divide cada linha em colunas (usando espaços ou delimitadores).

*   **Imprimir colunas específicas:** 
    `ls -l | awk '{print $9, $5}'` (Imprime o nome do arquivo e o tamanho).
*   **Usar um delimitador diferente (ex: dois pontos):** 
    `awk -F ":" '{print $1}' /etc/passwd` (Lista apenas os nomes dos usuários).
*   **Filtrar com lógica:** 
    `awk '$5 > 1000 {print $9}'` (Lista nomes de arquivos com mais de 1000 bytes).
*   **Somar valores de uma coluna:** 
    `awk '{soma += $5} END {print soma}' lista_vendas.txt`

---

## 🏗️ Exemplo Prático: O Combo (Pipe)
Você pode unir as três ferramentas para extrair informações complexas:

**Tarefa:** Ver quais IPs únicos acessaram seu servidor Nginx e quantas vezes:
```bash
cat /var/log/nginx/access.log | awk '{print $1}' | sort | uniq -c | sort -nr
```
*   `awk '{print $1}'`: Pega apenas a primeira coluna (o IP).
*   `sort`: Ordena para o `uniq` funcionar.
*   `uniq -c`: Conta as ocorrências.
*   `sort -nr`: Ordena numericamente do maior para o menor.

---

## 💡 Resumo de Escolha
*   Precisa **achar** algo? Use **Grep**.
*   Precisa **trocar** ou editar texto? Use **Sed**.
*   Precisa **processar colunas** ou fazer cálculos? Use **Awk**.

---
**Links Relacionados:**
- [[Linux]]
- [[Shell Scripting e Automação]]
- [[Troubleshooting no Linux]]
