# O que são Containers (Detalhes Técnicos)

Como vimos em [[Docker]], um contêiner é uma unidade de software isolada. Tecnicamente, um contêiner não é uma máquina virtual, mas sim um **processo isolado** rodando no kernel do host.

## 1. O Motor do Isolamento: Linux Namespaces e Cgroups

O Docker utiliza recursos do Kernel Linux para criar o isolamento:

*   **Namespaces:** Provê o isolamento de "visão" do processo. Cada contêiner acha que tem seu próprio sistema.
    *   `pid`: Isolamento de processos (o contêiner vê seu processo principal como PID 1).
    *   `net`: Interfaces de rede e portas próprias.
    *   `mnt`: Pontos de montagem de arquivos exclusivos.
    *   `uts`: Nome de host e domínio.
*   **Control Groups (Cgroups):** Responsável pela limitação de recursos. Garante que um contêiner não consuma toda a RAM ou CPU do host, causando o travamento de outros processos.

## 2. Imagem vs Contêiner

A relação entre eles é análoga à Programação Orientada a Objetos:
*   **Imagem:** É a "Classe". Um modelo somente-leitura (read-only) que contém o sistema de arquivos, bibliotecas e metadados.
*   **Contêiner:** É a "Instância". Uma execução daquela imagem que adiciona uma camada fina de escrita no topo.

## 3. Arquitetura de Camadas (Union File System)

O Docker utiliza um sistema de arquivos em camadas. Cada instrução no `Dockerfile` cria uma nova camada.

*   **Camadas de Imagem:** São imutáveis. Se você tem 10 contêineres rodando a mesma imagem de Python, todos compartilham as mesmas camadas de leitura no disco, economizando espaço.
*   **Copy-on-Write (CoW):** Quando um processo dentro do contêiner tenta modificar um arquivo da imagem, o Docker copia esse arquivo para a **Camada de Escrita** (Writable Layer) antes de modificá-lo. As camadas originais permanecem intactas.

## 4. Efemeridade e Persistência

Por padrão, os dados dentro de um contêiner são voláteis. Se o contêiner for removido, a *Camada de Escrita* é destruída. 

Para resolver isso e garantir a persistência (essencial para bancos de dados), utilizamos:
*   **Volumes:** Gerenciados pelo Docker, armazenados em uma área específica do host.
*   **Bind Mounts:** Mapeiam um diretório específico do seu computador para dentro do contêiner.

## 5. O Runtime (CRI)

O Docker não "roda" o contêiner sozinho. Ele utiliza componentes como o **containerd** e o **runc** para interagir com as chamadas de sistema do kernel e gerenciar o ciclo de vida dos contêineres conforme os padrões da OCI (Open Container Initiative).

---
**Veja também:**
- [[Docker]]
