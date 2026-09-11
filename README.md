# SvelteRP

An XRPL transaction lab built with SvelteKit: send Testnet XRP and understand exactly what happened.

```text
Create accounts → Send Testnet XRP → Validate → Explain changes
```

## Status

Planning only. No application code has been scaffolded.

## What it shows

- Sender and recipient balance changes
- Transaction fee
- Pending, validated, or failed status
- Raw transaction data
- Plain-English transaction explanation
- Common failures, such as insufficient funds or an incorrect sequence number

## Planned stack

- SvelteKit and Svelte
- TypeScript
- [xrpl.js](https://github.com/XRPLF/xrpl.js)
- XRPL Testnet and faucet
- WebSockets for live transaction updates
- Vitest for unit tests
- Playwright for full user-flow tests
- PostgreSQL only if saved experiments are added

Use SvelteKit for application structure and optional server endpoints. Keep account generation and transaction signing in the browser. Never send secret keys to the server or save them in PostgreSQL.

## Build stages

### 1. Payment inspector

Create two temporary Testnet accounts, fund them through the faucet, send XRP, and display the result.

Build components for account cards, a payment form, transaction status, balance changes, a raw JSON viewer, and a plain-English explanation.

### 2. Live validation

Use an XRPL WebSocket connection to update the interface as the transaction moves from submission to validation. Explore Svelte stores or runes for shared reactive state.

### 3. Failure playground

Let users intentionally trigger and inspect insufficient XRP, incorrect sequence numbers, invalid destinations, expired transactions, and unfunded destination requirements. Explain what failed and which transaction fields caused it.

### 4. Testnet token experiment

Create a fake token such as `HOOPS`. Demonstrate issuing a token, creating a trust line, sending the token, and comparing issued tokens with native XRP.

Keep everything on [XRPL Testnet](https://xrpl.org/docs/concepts/networks-and-servers/parallel-networks).

### 5. Optional AI explainer

Give an AI model normalized transaction data and ask it to explain the result at beginner or developer depth. Calculate fees, balances, delivered amounts, and status in TypeScript. Use AI only to explain those established facts.

## Suggested future structure

```text
src/
├── lib/
│   ├── components/
│   ├── xrpl/
│   │   ├── client.ts
│   │   ├── accounts.ts
│   │   ├── payments.ts
│   │   └── normalize-transaction.ts
│   ├── stores/
│   └── types/
├── routes/
│   ├── +page.svelte
│   ├── transaction/
│   └── api/
└── tests/
```

Keep XRPL logic separate from Svelte components so the blockchain code is easier to test and reuse.

## First milestone

A two-weekend version should let someone:

1. Generate two Testnet accounts.
2. Send XRP between them.
3. Watch the transaction become validated.
4. Compare balances before and after.
5. Read both the raw metadata and a useful explanation.

This milestone demonstrates Svelte, TypeScript, WebSockets, testing, data normalization, and blockchain interaction.
