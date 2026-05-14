# Monitoramento e Logging

A observabilidade é crucial para entender o estado interno de um sistema através de seus outputs externos.

## Os Três Pilares da Observabilidade
1. **Logs**: Registros de eventos discretos (imutáveis e com timestamp).
2. **Métricas**: Agregados numéricos sobre um período de tempo.
3. **Traces**: Rastreamento do ciclo de vida de uma requisição através de microserviços.

## 🚀 Monitoramento Avançado (APM)
O **APM (Application Performance Monitoring)** foca na experiência do usuário e na saúde da aplicação, indo além da infraestrutura.
* **Métricas de Ouro (Golden Signals)**: Latência, Tráfego, Erros e Saturação.
* **Profiling**: Análise de consumo de CPU e memória em nível de linha de código.
* **Ferramentas**: New Relic, Dynatrace, Datadog e **OpenTelemetry** (alternativa open-source).

## 🔔 Sistemas de Alerta
Monitorar sem alertar é apenas observar o passado. Um bom sistema de alerta deve ser acionável.
* **Prometheus Alertmanager**: Gerencia alertas enviados pelo Prometheus, tratando silenciamentos, inibições e notificações via Slack, PagerDuty ou Email.
* **SLAs, SLOs e SLIs**:
    - **SLI (Indicator)**: O que você mede (ex: latência).
    - **SLO (Objective)**: A meta (ex: latência < 200ms em 99% das vezes).
    - **SLA (Agreement)**: O contrato de negócio baseado no SLO.

## Stack de Ferramentas
* **ELK Stack (Elasticsearch, Logstash, Kibana)**: Tradicional para centralização de logs.
* **PLG Stack (Prometheus, Loki, Grafana)**: Alternativa moderna e eficiente em recursos.
* **OpenTelemetry**: Padrão aberto para coleta de dados de observabilidade.
* **Jaeger**: Ferramenta para tracing distribuído.
