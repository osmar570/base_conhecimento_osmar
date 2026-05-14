# Serverless e Edge Computing

Novos paradigmas de computação que visam reduzir a gestão de infraestrutura e aproximar o processamento do usuário.

## Serverless (FaaS/BaaS)

### ⚡ FaaS (Function as a Service)
Execução de código em resposta a eventos sem gerenciar servidores.
* **AWS Lambda**: O pioneiro, altamente integrado ao ecossistema AWS (S3, DynamoDB, SQS).
* **Azure Functions**: Excelente suporte para .NET e integração com Azure AD e Service Bus.
* **Google Cloud Functions**: Focado em simplicidade e integração com o Firebase e GCP Pub/Sub.
* **Características**: Escalabilidade automática de zero ao infinito, modelo de cobrança por execução (Pay-per-use).

### 🗄️ BaaS (Backend as a Service)
Uso de serviços de terceiros para gerenciar lógica e persistência de backend.
* **Firebase (Google)**: Autenticação, banco de dados em tempo real (Firestore) e hosting.
* **Supabase**: Alternativa open-source ao Firebase, baseada em PostgreSQL.
* **Auth0**: Especialista em Gestão de Identidade (IAM).

## 🌐 Edge Computing
Processamento de dados na "borda" da rede, mais perto da fonte dos dados.
* **Edge Workers**: Execução de lógica simples em CDNs (ex: **Cloudflare Workers**, AWS Lambda@Edge).
* **Casos de Uso**: Redução de latência para usuários globais, processamento de dados IoT antes de enviar para a nuvem, manipulação de imagens on-the-fly.
