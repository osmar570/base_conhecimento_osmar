# Processos e Monitoramento do Sistema

No Linux, cada programa em execução é chamado de **Processo**. O Kernel gerencia esses processos, atribuindo a cada um um número de identificação único chamado **PID** (Process ID).

---

## 1. Visualizando Processos

Existem várias ferramentas para ver o que está rodando:

| Comando | Descrição |
| :--- | :--- |
| `ps aux` | Tira um "retrato" estático de todos os processos do sistema. |
| `top` | Mostra os processos em tempo real (nativo do Linux). |
| `htop` | Uma versão muito mais amigável e colorida do `top` (precisa ser instalado). |
| `pstree` | Exibe os processos em formato de árvore, mostrando quem criou quem. |

---

## 2. Gerenciando Processos (Matar e Priorizar)

Às vezes, um processo trava ou consome CPU demais e precisa ser encerrado.

*   **`kill <PID>`**: Envia um sinal suave para o processo fechar (SIGTERM).
*   **`kill -9 <PID>`**: Envia um sinal forçado (SIGKILL). Use apenas se o anterior não funcionar.
*   **`pkill <nome>`**: Mata processos pelo nome em vez do PID.
*   **`killall <nome>`**: Mata todas as instâncias de um programa pelo nome.

### Prioridade (Nice)
O Linux permite definir quais processos são mais importantes:
*   **`nice`**: Inicia um programa com uma prioridade específica.
*   **`renice`**: Altera a prioridade de um processo que já está rodando.
*(Valores vão de -20 (mais prioritário) a 19 (menos prioritário)).*

---

## 3. Monitoramento de Recursos (Hardware)

Além dos processos, precisamos monitorar o "corpo" do computador:

### Memória RAM
*   **`free -h`**: Exibe a memória total, usada e livre em formato legível (GB/MB).

### Disco Rígido
*   **`df -h`**: Mostra o espaço total e disponível em todas as partições do disco.
*   **`du -sh <pasta>`**: Calcula o tamanho total de uma pasta específica.

### Rede
*   **`ss -tulpn`**: Mostra todas as portas e conexões de rede ativas.
*   **`nload`**: Monitora o tráfego de rede em tempo real.

---

## 4. Processos em Segundo Plano (Background)

Você pode rodar comandos sem travar o seu terminal:

*   **`comando &`**: Inicia o comando direto em background.
*   **`CTRL + Z`**: Pausa um comando que está rodando.
*   **`bg`**: Move o comando pausado para o background.
*   **`fg`**: Traz o comando do background de volta para o primeiro plano.
*   **`jobs`**: Lista os processos que estão rodando em background no seu terminal atual.
*   **`nohup <comando> &`**: Garante que o comando continue rodando mesmo que você feche o terminal/desconecte do SSH.

---

## 💡 Cenário Comum (Troubleshooting)
Sua máquina está lenta?
1.  Abra o `htop`.
2.  Pressione `F6` para ordenar por `%CPU`.
3.  Identifique o PID do culpado.
4.  Pressione `F9` para enviar um `SIGTERM` ou `SIGKILL`.

---
**Links Relacionados:**
- [[Linux]]
- [[Comandos Essenciais de Terminal]]
- [[Troubleshooting no Linux]]
