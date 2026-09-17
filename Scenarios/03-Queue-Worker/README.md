# 3 — Backend → Fila → Worker ✅⚠️

> CENA 5 · só slide, não é construído no vídeo.

```
Cliente → API → Queue → Worker → SMTP
```

## O que resolve — o grande salto conceitual
- **Desacoplamento temporal** — produtor e consumidor não precisam estar online ao mesmo tempo.
- **Buffer / back-pressure** — no pico a fila absorve a carga; o worker consome no ritmo dele.
- **Retry** — a mensagem fica na fila até alguém processá-la.
- A API publica e responde **na hora**.

## A dor que sobra
O worker continua sendo um processo **ligado 24h por dia** — VM, container ou Pod. Alguém precisa provisionar, atualizar, monitorar, configurar escala e **pagar mesmo quando não há e-mail para enviar**.

## Próximo passo
→ [`04-ServiceBus-Function`](../04-ServiceBus-Function) — o consumidor vira serverless.

## Código
Não há código neste cenário. Ele é o cenário 4 com o consumidor rodando como processo fixo em vez de Function; o contrato e o produtor são os mesmos de [`../04-ServiceBus-Function/BackendApi`](../04-ServiceBus-Function/BackendApi).
