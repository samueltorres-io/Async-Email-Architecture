# 4 — Service Bus → Azure Function → ACS 🏆

> CENAS 6, 9, 11–15 · **esta é a única arquitetura construída no vídeo.**

```
┌──────────────────────────┐
│  Frontend + API           │   ← só PUBLICA um evento
└────────────┬─────────────┘
             │  EmailRequest (JSON)
             ▼
┌──────────────────────────┐
│   Azure Service Bus Queue │   ← buffer, DLQ, duplicate detection
└────────────┬─────────────┘
             │  ServiceBusTrigger
             ▼
┌──────────────────────────┐
│  Azure Function (Bun/TS)  │   ← consumidor serverless + Handlebars
└────────────┬─────────────┘
             │  SDK do ACS
             ▼
┌──────────────────────────┐
│  Azure Communication      │   ← PROVEDOR de envio
│  Services — Email         │
└──────────────────────────┘
```

## O que muda em relação ao cenário 3
O worker 24h vira uma **Azure Function** acionada automaticamente pela mensagem na fila. Sem servidor para gerenciar, escala sozinha, paga só pelas execuções.

**Duas camadas diferentes** (ponto que passa senioridade):
- **Azure Function** = a computação (o consumidor). Gatilho: `ServiceBusTrigger`.
- **ACS Email** = o provedor de envio (entrega de fato; substitui SMTP/SendGrid).

## O que está aqui
- [`BackendApi/`](./BackendApi) — o **produtor**. Formulário + `POST /email` → publica `EmailRequest` no Service Bus → responde **202 Accepted**. Autentica com Managed Identity (`DefaultAzureCredential`), sem connection string no código.

## O que NÃO está aqui
- A **Function** (consumidor) é única em todo o repositório: [`../../Infrastructure/Azure/EmailFunction`](../../Infrastructure/Azure/EmailFunction).
- O provisionamento dos recursos Azure: [`../../Infrastructure/Bicep`](../../Infrastructure/Bicep).

## Contrato
`EmailRequest` é o coração da arquitetura: destinatário, assunto, corpo (+ `templateId` / `data` para o Handlebars). API e Function nunca se chamam diretamente — a única coisa que elas concordam entre si é o formato dessa mensagem. Campo novo entra mantendo compatibilidade.
