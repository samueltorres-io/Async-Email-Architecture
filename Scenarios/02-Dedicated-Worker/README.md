# 2 — Worker / serviço de e-mail dedicado ⚠️

> CENA 4 · só slide, não é construído no vídeo.

```
Cliente → API → Email API/Worker → SMTP
```

## O que resolve
**Separação de responsabilidade.** A API não cuida mais de e-mail; existe um serviço especializado só para isso.

## A dor que continua
- A chamada API → worker ainda é **direta e síncrona** (HTTP). Se o worker está sobrecarregado ou fora do ar, a chamada falha — mesmo problema do cenário 1, só que mais longe.
- **Acoplamento temporal**: os dois serviços precisam estar de pé ao mesmo tempo.
- Sem buffer, sem retry natural.
- Mais uma aplicação para desenvolver, monitorar, escalar e pagar (Auto Scaling + Load Balancer crescem junto com a demanda).

## Próximo passo
→ [`03-Queue-Worker`](../03-Queue-Worker) — comunicação assíncrona.

## Código
Não há código neste cenário. É uma variação de infraestrutura do cenário 1, não de arquitetura de código.
