# Benchmarks

Medições que sustentam com número o que o roteiro afirma com narrativa.

## O que medir

| # | Comparação | Métrica | Sustenta |
|---|---|---|---|
| 1 | Envio síncrono (arq. 1) **vs.** publicar na fila (arq. 4) | latência do endpoint: p50, p95, p99 | CENA 3 — "a latência explode" / CENA 12 — o 202 Accepted |
| 2 | Mesmo teste sob carga crescente (100 → 1k → 10k req) | throughput + taxa de erro/timeout | CENA 3 — "o checkout cai junto" |
| 3 | Provedor de e-mail indisponível | requests com falha em cada arquitetura | CENA 3 vs. CENA 5 — a fila como buffer |
| 4 | Cold start da Function | tempo até a 1ª execução, frio vs. quente | CENA 15 — o cold start honesto |

O ponto do benchmark 3 é o mais forte: na arquitetura 1 o checkout falha junto; na 4 a mensagem só espera na fila.

## Como rodar
Ferramenta: `k6` ou `bombardier` contra o `BackendApi`, com o envio síncrono e o assíncrono atrás de um flag, para comparar o mesmo código nas duas pontas.

> ⚠️ Cenário 1 não tem código construído (é slide). Para medir, sobe-se uma variante do [`BackendApi`](../../Scenarios/04-ServiceBus-Function/BackendApi) enviando direto via SMTP/ACS.

## Saída
- Números brutos e análise: aqui.
- Gráficos gerados: [`Assets/Benchmark-Charts/`](../../Assets/Benchmark-Charts).

## Onde entra no vídeo
Ainda **não há cena para isso no roteiro**. Os candidatos naturais são o fim da CENA 3 (mostrar o p95 estourando dá peso à dor) ou a CENA 15, logo após a demo end-to-end.
