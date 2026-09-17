# Cenários

Cada pasta corresponde a uma arquitetura do vídeo, na mesma ordem das cenas.

| # | Pasta | Cena | Construído? | Backend |
|---|---|---|---|---|
| 1 | `01-Direct-Send` | CENA 3 | ❌ só slide | — |
| 2 | `02-Dedicated-Worker` | CENA 4 | ❌ só slide | — |
| 3 | `03-Queue-Worker` | CENA 5 | ❌ só slide | — |
| 4 | `04-ServiceBus-Function` | CENAS 6, 9, 12–15 | ✅ | `BackendApi/` |

**Regra de organização:**

- Cenário com backend próprio → o código fica em `<cenario>/BackendApi/`.
- Cenário que não altera o backend → só `README.md`, explicando a arquitetura e apontando para o código de referência.
- **A Function é única** e vive em [`Infrastructure/Azure/EmailFunction`](../Infrastructure/Azure/EmailFunction). Ela não é duplicada por cenário: só existe na arquitetura 4.
