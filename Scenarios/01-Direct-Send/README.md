# 1 — Envio direto no backend ❌

> CENA 3 · só slide, não é construído no vídeo.

```
Cliente → API → SMTP
```

## O que é
A própria API envia o e-mail dentro do fluxo da request. Uma thread fica bloqueada esperando o SMTP responder antes de devolver a resposta ao usuário.

## Quando funciona
Até ~100 usuários / 100–200 e-mails transacionais por dia. Simples, rápido de implementar, totalmente válido nesse contexto.

## A dor
- **Acoplamento** — o tempo de resposta da API passa a depender de um sistema externo que você não controla.
- **Operação síncrona bloqueante** — o usuário espera por algo que ele não precisaria esperar; o pedido já foi feito.
- Se o SMTP cai, o **checkout cai junto**.

## Próximo passo
→ [`02-Dedicated-Worker`](../02-Dedicated-Worker) — tirar o envio de e-mail de dentro da API.

## Código
Não há código neste cenário. O backend de referência (produtor) está em [`../04-ServiceBus-Function/BackendApi`](../04-ServiceBus-Function/BackendApi) — a diferença é que lá ele publica na fila em vez de enviar o e-mail.
