# Async Email Architecture

Repositório do vídeo **"Pare de Enviar E-mails Direto da API: Arquitetura Profissional com Azure"**.

Quatro arquiteturas que resolvem o mesmo problema — enviar e-mail transacional — de formas cada vez menos acopladas. Cada uma resolve a dor da anterior e cria uma nova.

```
Frontend + API (.NET 8)  →  Azure Service Bus  →  Azure Function (Bun + TS)  →  ACS Email
      PRODUTOR                  DESACOPLAMENTO         CONSUMIDOR                PROVEDOR
```

## Onde está cada coisa

| Pasta | Conteúdo |
|---|---|
| [`Scenarios/`](./Scenarios) | As 4 arquiteturas. Só a 4ª tem código; as outras têm README explicando a dor. |
| [`Infrastructure/Azure/EmailFunction/`](./Infrastructure/Azure/EmailFunction) | A Azure Function (Bun + TypeScript + Handlebars). **Única no repo.** |
| [`Infrastructure/Bicep/`](./Infrastructure/Bicep) | Provisionamento dos recursos Azure. |
| [`Docs/Video/SCRIPT.md`](./Docs/Video/SCRIPT.md) | Roteiro cena a cena. |
| [`Docs/Architecture/`](./Docs/Architecture) | Notas de arquitetura e decisões (ADRs). |
| [`Docs/Benchmarks/`](./Docs/Benchmarks) | Medições de latência/throughput que sustentam a narrativa com número. |
| [`Assets/Diagrams/`](./Assets/Diagrams) | Diagramas usados nos slides. |

## Conceitos cobertos
Acoplamento · acoplamento temporal · comunicação assíncrona · mensageria · event-driven · serverless · back-pressure · at-least-once delivery · idempotência · DLQ · poison message · Managed Identity · observabilidade · trade-off de custo
