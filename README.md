# Verifiable Agent Marketplace

An autonomous AI agent that pays for the tools and data it uses, and sells its own inference the same way — with cryptographic proof that the output actually came from the model it claims to.

## Why this project

AI x crypto has shifted in 2026 from speculative token narratives toward real infrastructure. Two things are converging:

- **Agentic payments** — Coinbase's [x402](https://docs.cdp.coinbase.com/x402/) protocol lets an AI agent pay for an API call in the moment, using the HTTP 402 status code: a server quotes a price in a stablecoin, the agent checks it against its own budget, and a facilitator settles the payment on-chain.
- **Verifiable inference** — as agents start moving real money based on model outputs, "trust me" is no longer good enough. Running inference inside a trusted execution environment (or producing a ZKML proof) lets a caller verify that a specific model produced a specific output for a specific input.

This project builds a small agent economy around both ideas: a consumer agent that shops for and pays for tools within a budget, and a provider agent that sells verifiable inference per call.

## Architecture

```
Consumer agent (budgeted wallet)
        │
        ▼
x402 paywalled request (HTTP 402 + price quote)
        │
        ▼
Facilitator (verifies payment, settles USDC on-chain)
        │
        ▼
Provider agent (runs the model inside a TEE, signs an attestation)
        │
        ▼
Verified response (output + proof, logged on-chain) ──▶ back to consumer
```

## Roadmap

- [ ] Stand up wallets and a working x402 payment (testnet, Base Sepolia)
- [ ] Build the consumer agent (budget-aware, tool-selecting)
- [ ] Build the provider side — sell inference behind an x402-gated endpoint
- [ ] Add verifiability — TEE attestation (Phala / Marlin) or a ZKML proof (EZKL) on the provider side
- [ ] Log transactions and add a small dashboard for payment + verification flow
- [ ] Optional: on-chain Solidity contract (reputation registry or attestation-gated escrow)
- [ ] Polish: public testnet demo, technical writeup, short demo video

## Tech stack (planned)

- **Agents:** LangChain / LangGraph or CrewAI (or a hand-rolled tool-use loop)
- **Payments:** x402 protocol, Coinbase CDP AgentKit, USDC on Base Sepolia (testnet)
- **Verifiability:** Phala Cloud or Marlin (TEE attestation), optionally EZKL (ZKML)
- **Contracts (optional):** Solidity, Foundry
- **Frontend:** lightweight dashboard for transaction + verification visibility

## Status

Early scaffolding. README and roadmap only — implementation in progress.

## License

MIT
