# EmailFunction — o consumidor

**Azure Function única de todo o repositório.** Ela só existe na arquitetura 4 ([`Scenarios/04-ServiceBus-Function`](../../../Scenarios/04-ServiceBus-Function)) e por isso não é duplicada dentro das pastas de cenário.

## Stack
- **Bun + TypeScript** (Azure Functions, custom handler / Node runtime)
- **Handlebars** para compilar os templates de e-mail
- **`@azure/communication-email`** para o envio
- **Managed Identity** (`DefaultAzureCredential`) para acessar fila e ACS — sem segredo no código

## O que ela faz
1. É acordada pelo `ServiceBusTrigger` na fila `emails`.
2. Desserializa o `EmailRequest`.
3. Compila o template correspondente com Handlebars.
4. Entrega via ACS Email.

Ela **não envia o e-mail** — orquestra. Quem entrega é o Communication Services.

## Falha
Exceção → Service Bus re-entrega (retry) → após `MaxDeliveryCount` → **DLQ**. Por isso o handler precisa ser **idempotente** (`MessageId` já processado / duplicate detection do Service Bus): a entrega é *at-least-once*.

## Estrutura
```
src/
├── templates/     → templates .hbs (texto, HTML+CSS, HTML com imagem inline via CID)
└── ...            → handler + envio via ACS
```

## Anexos
Anexo grande não vai dentro da mensagem da fila (Service Bus tem limite de tamanho e o ACS cobra por dados). Vai para o Blob Storage e a mensagem carrega só o link/SAS.
