# Infrastructure

| Pasta | O que é |
|---|---|
| [`Azure/EmailFunction`](./Azure/EmailFunction) | O código da Azure Function (consumidor). Única no repo — ver o README de lá. |
| [`Bicep`](./Bicep) | Provisionamento dos recursos: Resource Group, Service Bus namespace + queue `emails`, ACS Email (domínio gerenciado), Function App, Application Insights, Storage. |

No vídeo, a fila é criada **ao vivo** pelo portal (CENA 11); o resto já vem provisionado. O Bicep aqui serve para quem clonar o repo subir tudo de uma vez.
