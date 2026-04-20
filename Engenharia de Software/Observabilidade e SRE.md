# Observabilidade e SRE (Site Reliability Engineering)

A observabilidade é a capacidade de entender o estado interno de um sistema complexo apenas observando seus outputs (métricas, logs e traces). Em ambientes Cloud-Native, ela é o que permite diagnosticar problemas que você não previu que aconteceriam.

---

## 🏛️ Os Três Pilares

### 1. Métricas (Metrics)
Representações numéricas de dados medidos em intervalos de tempo.
- **Tipos:** Contadores (incrementais), Gauges (valor atual), Histogramas (distribuição).
- **Utilidade:** Dashboards de saúde e alertas de infraestrutura.
- **Exemplo:** `http_requests_total`, `node_memory_usage_bytes`.

### 2. Logs
Registros imutáveis de eventos individuais.
- **Boas Práticas:** Use **Structured Logging** (JSON) para facilitar a consulta por ferramentas de agregação.
- **Utilidade:** Diagnóstico profundo e auditoria.
- **Exemplo:** `{"level": "error", "message": "database connection timeout", "service": "order-api", "trace_id": "abc-123"}`.

### 3. Rastreamento Distribuído (Distributed Tracing)
Mapeia a jornada de uma requisição através de vários componentes.
- **Span:** A menor unidade de trabalho (ex: uma query SQL ou uma chamada HTTP).
- **Trace:** Coleção de spans que formam o fluxo completo.
- **Utilidade:** Identificar qual microsserviço está causando lentidão em um fluxo de negócio.

---

## 🛰️ SRE: Site Reliability Engineering

SRE é a disciplina que aplica práticas de engenharia de software para resolver problemas de operações.

### Conceitos Chave:
- **SLI (Service Level Indicator):** A métrica real medida (ex: latência de 99% das reqs < 200ms).
- **SLO (Service Level Objective):** A meta de desempenho baseada no SLI (ex: 99.9% de disponibilidade no mês).
- **SLA (Service Level Agreement):** O contrato legal com o cliente (geralmente baseado no SLO).
- **Error Budget:** A margem de erro aceitável (100% - SLO). Se o orçamento acaba, o foco do time muda de "novas features" para "estabilidade".

---

## ⚙️ Observabilidade em Software (Práticas)

### Health Checks (Kubernetes)
O software deve informar seu estado para o orquestrador:
- **Liveness Probe:** "Estou vivo?". Se falhar, o K8s reinicia o container.
- **Readiness Probe:** "Estou pronto para receber tráfego?". Se falhar, o K8s remove do Service.
- **Startup Probe:** Usada para apps que demoram a iniciar.

### Graceful Shutdown
O software deve ser capaz de encerrar processos e fechar conexões de banco de dados ao receber um sinal de terminação (`SIGTERM`), garantindo que nenhuma requisição seja perdida durante um deploy ou escala.

---
**Links Relacionados:**
- [[Kubernetes]] (Onde os sinais de ouro e probes são monitorados)
- [[Docker]] (Conceitos de isolamento de recursos)
- [[Clean Architecture]] (Onde os logs e métricas de negócio devem ser injetados)
