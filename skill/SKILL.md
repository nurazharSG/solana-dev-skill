---
name: solana-dev
description: End-to-end Solana development playbook (Jan 2026). Prefer Solana Foundation framework-kit (@solana/client + @solana/react-hooks) for React/Next.js UI. Prefer @solana/kit for all new client/RPC/transaction code. When legacy dependencies require web3.js, isolate it behind @solana/web3-compat (or @solana/web3.js as a true legacy fallback). Covers wallet-standard-first connection (incl. ConnectorKit), Anchor/Pinocchio/Steel programs, Codama-based client generation, Bankrun/Surfpool testing, and security checklists.
user-invocable: true
---

# Solana Development Skill (framework-kit-first)

## What this Skill is for
Use this Skill when the user asks for:
- Solana dApp UI work (React / Next.js)
- Wallet connection + signing flows
- Transaction building / sending / confirmation UX
- On-chain program development (Anchor or native Rust)
- Client SDK generation (typed program clients)
- Local testing (Bankrun, Surfpool, test-validator)
- Security hardening and audit-style reviews

## Default stack decisions (opinionated)
1) **UI: framework-kit first**
- Use `@solana/client` + `@solana/react-hooks`.
- Prefer Wallet Standard discovery/connect via the framework-kit client.

2) **SDK: @solana/kit first**
- Prefer Kit types (`Address`, `Signer`, transaction message APIs, codecs).
- Prefer `@solana-program/*` instruction builders over hand-rolled instruction data.

3) **Legacy compatibility: web3.js only at boundaries**
- If you must integrate a library that expects web3.js objects (`PublicKey`, `Transaction`, `Connection`),
  use `@solana/web3-compat` as the boundary adapter.
- Do not let web3.js types leak across the entire app; contain them to adapter modules.

4) **Programs**
- Default: Anchor.
- Performance/footprint: Pinocchio or Steel only when there's an explicit need (CU/binary size, no_std,
  reduced dependencies, or strict control over parsing/allocations).

5) **Testing**
- Default: Bankrun for unit tests (fast feedback).
- Use Surfpool for integration tests against realistic cluster state (mainnet/devnet) locally.
- Use solana-test-validator only when you need "real RPC node behavior" that bankrun doesn't emulate.

## Operating procedure (how to execute tasks)
When solving a Solana task:

### 1. Classify the task layer
- UI/wallet/hook layer
- Client SDK/scripts layer
- Program layer (+ IDL)
- Testing/CI layer
- Infra (RPC/indexing/monitoring)

### 2. Pick the right building blocks
- UI: framework-kit patterns.
- Scripts/backends: @solana/kit directly.
- Legacy library present: introduce a web3-compat adapter boundary.

### 3. Implement with Solana-specific correctness
Always be explicit about:
- cluster + RPC endpoints + websocket endpoints
- fee payer + recent blockhash
- compute budget + prioritization (where relevant)
- expected account owners + signers + writability
- token program variant (SPL Token vs Token-2022) and any extensions

### 4. Add tests
- Unit test: Bankrun.
- Integration test: Surfpool or test-validator.
- For "wallet UX", add mocked hook/provider tests where appropriate.

### 5. Deliverables expectations
When you implement changes, provide:
- exact files changed + diffs (or patch-style output)
- commands to install/build/test
- a short "risk notes" section for anything touching signing/fees/CPIs/token transfers

## Progressive disclosure (read when needed)
- UI + wallet + hooks: [frontend-framework-kit.md](frontend-framework-kit.md)
- Kit ↔ web3.js boundary: [kit-web3-interop.md](kit-web3-interop.md)
- Anchor programs: [programs-anchor.md](programs-anchor.md)
- Native programs (Pinocchio/Steel): [programs-native.md](programs-native.md)
- Testing strategy: [testing.md](testing.md)
- IDLs + codegen: [idl-codegen.md](idl-codegen.md)
- Payments: [payments.md](payments.md)
- Security checklist: [security.md](security.md)
- Reference links: [resources.md](resources.md)
