# WebSockets e Comunicação Real-time

WebSockets fornecem um canal de comunicação bidirecional e full-duplex sobre uma única conexão TCP de longa duração.

## 🔄 Como Funciona
1. **Handshake**: O cliente envia uma requisição HTTP com o header `Upgrade: websocket`.
2. **Upgrade**: Se o servidor suportar, ele responde com o status `101 Switching Protocols`.
3. **Conexão Persistente**: A conexão TCP permanece aberta, permitindo o envio de mensagens de ambos os lados sem o overhead do HTTP.

## 🎯 Casos de Uso
* **Chats e Mensageiros**: Mensagens instantâneas.
* **Dashboards em Tempo Real**: Atualização de gráficos e métricas sem refresh.
* **Jogos Multiplayer**: Sincronização de estado entre jogadores.
* **Ferramentas Colaborativas**: Edição simultânea de documentos (ex: Google Docs).

## 🛡️ Desafios e Considerações
* **Escalabilidade**: Manter milhares de conexões abertas exige gestão de memória e o uso de "Sticky Sessions" ou Pub/Sub (Redis) para sincronizar múltiplos servidores.
* **Segurança**: WebSockets não seguem a mesma política de Same-Origin do REST; é necessário validar origens e tokens no handshake.
* **Fallback**: Em redes restritas, pode ser necessário o uso de *Long Polling* (ex: via Socket.io).
