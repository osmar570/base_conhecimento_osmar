# Mensageria e Sistemas Event-Driven

A mensageria é um padrão de comunicação assíncrona onde os sistemas trocam informações através de mensagens intermediadas por um **Message Broker**. É a base para a criação de arquiteturas desacopladas e resilientes.

---

## 🏗️ Conceitos Fundamentais do RabbitMQ

Para dominar o RabbitMQ, é preciso entender como as mensagens fluem dentro do Broker:

1.  **Producer (Produtor):** A aplicação que envia a mensagem. Ela nunca envia diretamente para uma fila, mas sim para uma **Exchange**.
2.  **Exchange (Câmbio):** Recebe mensagens do produtor e as roteia para as filas baseada em regras (Routing Keys).
    - **Direct:** Roteia para a fila que tem a chave de roteamento exata.
    - **Fanout:** Roteia para todas as filas conectadas (broadcast).
    - **Topic:** Roteia baseado em padrões (ex: `pedidos.*`).
3.  **Queue (Fila):** Onde as mensagens ficam armazenadas até que um consumidor as processe.
4.  **Binding (Ligação):** A regra que conecta uma Exchange a uma Queue.
5.  **Consumer (Consumidor):** A aplicação que fica "escutando" a fila para processar os dados.

---

## 🚀 Implementação com C# (.NET)

Para os exemplos abaixo, utilize o pacote NuGet: `RabbitMQ.Client`.

### 1. Criando Infraestrutura Automaticamente (Setup)
É boa prática que o sistema garanta que as filas e exchanges existam ao iniciar.

```csharp
using RabbitMQ.Client;

var factory = new ConnectionFactory() { HostName = "localhost" };
using var connection = factory.CreateConnection();
using var channel = connection.CreateModel();

// 1. Declarar a Exchange
channel.ExchangeDeclare(exchange: "vendas.events", type: ExchangeType.Topic);

// 2. Declarar a Fila
// durable: true garante que a fila sobreviva ao restart do Broker
channel.QueueDeclare(queue: "vendas.fila.email", durable: true, exclusive: false, autoDelete: false);

// 3. Criar o Binding (Ligar a fila na exchange com uma rota específica)
channel.QueueBind(queue: "vendas.fila.email", 
                  exchange: "vendas.events", 
                  routingKey: "venda.confirmada");
```

### 2. Publicando uma Mensagem (Producer)
```csharp
var message = "{ \"id\": 123, \"status\": \"pago\" }";
var body = Encoding.UTF8.GetBytes(message);

channel.BasicPublish(exchange: "vendas.events",
                     routingKey: "venda.confirmada",
                     basicProperties: null,
                     body: body);
```

### 3. Escutando uma Fila (Consumer)
O consumidor deve rodar como um `BackgroundService` em .NET.

```csharp
using RabbitMQ.Client.Events;

var consumer = new EventingBasicConsumer(channel);
consumer.Received += (model, ea) => {
    var body = ea.Body.ToArray();
    var message = Encoding.UTF8.GetString(body);
    
    try {
        Console.WriteLine($"Processando: {message}");
        // Acknowledge: Confirma que processou com sucesso
        channel.BasicAck(ea.DeliveryTag, multiple: false);
    } catch (Exception) {
        // Nack: Rejeita e coloca de volta na fila (requeue: true)
        channel.BasicNack(ea.DeliveryTag, multiple: false, requeue: true);
    }
};

channel.BasicConsume(queue: "vendas.fila.email", autoAck: false, consumer: consumer);
```

---

## 🛡️ Idempotência e Resiliência
- **Idempotência:** Como uma mensagem pode ser entregue mais de uma vez (em caso de falha de rede no ACK), seu consumidor deve verificar se já processou aquele ID de mensagem antes de executar a lógica de negócio.
- **Retry Policy:** Use bibliotecas como **Polly** para tentar processar a mensagem novamente antes de enviá-la para uma **Dead Letter Queue (DLQ)**.

---
**Links Relacionados:**
- [[02. Engenharia de Software/Design Patterns/Comportamentais/Observer|Padrão Observer]]
- [[05. Trilhas de Estudos/Desenvolvedor CSharp - Senior|Trilha Sênior .NET]]
