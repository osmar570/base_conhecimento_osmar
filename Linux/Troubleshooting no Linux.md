# Troubleshooting no Linux

Depurar problemas no Linux exige uma abordagem metódica. Este guia reúne os passos e comandos essenciais para identificar e resolver as falhas mais comuns no sistema.

---

## 1. Analisando a Saúde do Sistema (Logs)

O Linux registra quase tudo o que acontece. Os logs são seu primeiro ponto de parada.

*   **`journalctl -xe`**: Mostra os erros mais recentes do sistema (systemd).
*   **`journalctl -u <serviço>`**: Filtra logs de um serviço específico (ex: `docker`).
*   **`dmesg -T`**: Mostra mensagens do Kernel (erros de hardware, drivers, falta de memória).
*   **`tail -f /var/log/syslog`**: Acompanha em tempo real as mensagens gerais do sistema.

---

## 2. Falhas em Serviços (`systemctl`)

Se um programa (Nginx, Docker, SSH) não inicia ou parou de responder:

1.  **Verifique o Status:** `systemctl status <serviço>` (Procure por linhas em vermelho).
2.  **Tente Reiniciar:** `sudo systemctl restart <serviço>`.
3.  **Verifique se a porta está ocupada:** `sudo ss -tulpn | grep <porta>`.

---

## 3. Problemas de Performance (CPU e RAM)

Sua máquina está lenta ou "congelando"?

*   **Processo consumindo 100%:** Use `htop` ou `top`. Pressione `P` para ordenar por CPU.
*   **Falta de Memória (OOM):** Verifique se o Kernel matou processos para liberar RAM com `dmesg | grep -i "out of memory"`.
*   **Uso de Swap:** `free -h` (Se o swap estiver alto, sua RAM física acabou).

---

## 4. Problemas de Disco (Armazenamento)

Muitas vezes o sistema para de funcionar porque o disco encheu.

*   **Verificar espaço:** `df -h` (Procure por partições com 100% de uso).
*   **Achar pastas pesadas:** `sudo du -sh /* | sort -h`.
*   **Arquivos abertos deletados:** Às vezes você deleta um log mas o espaço não libera. Use `sudo lsof +L1` para achar processos segurando arquivos deletados.

---

## 5. Falhas de Rede e Conectividade

*   **DNS não resolve:** Teste com `dig google.com` ou `nslookup`. Verifique o arquivo `/etc/resolv.conf`.
*   **Host inacessível:** Tente `ping` e depois `traceroute` para ver onde o pacote está parando.
*   **Firewall bloqueando:** Verifique o UFW (`sudo ufw status`) ou IPTables (`sudo iptables -L`).

---

## 6. O Sistema não dá Boot (Modo de Recuperação)

Se o Linux não inicia:

1.  **Grub:** Tente selecionar versões anteriores do Kernel no menu de boot.
2.  **Live USB:** Se nada funcionar, dê boot por um pendrive, monte suas partições com `mount` e use o comando `chroot` para "entrar" no seu sistema e consertar os arquivos de configuração.

---
**Links Relacionados:**
- [[Linux]] (Início)
- [[Processos e Monitoramento]]
- [[Redes no Linux]]
- [[Comandos Essenciais de Terminal]]
