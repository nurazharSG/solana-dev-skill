# Solana security checklist (program + client)

## Core principle
Assume the attacker controls:
- every account passed into an instruction
- every instruction argument
- transaction ordering (within reason)
- CPI call graphs (via composability)

## Program-side checklist
### Account validation
- Validate account owners (program id / token program id / metadata program id).
- Validate signer requirements explicitly.
- Validate writable requirements explicitly.
- Validate that PDAs match expected seeds + bump.
- Validate token mint ↔ token account relationships and authorities.
- Validate rent exemption / account initialization expectations where relevant.

### CPI safety
- Avoid arbitrary CPI targets unless explicitly designed.
- Do not pass extra writable or signer privileges to CPI callees.
- Ensure invoke_signed seeds are correct and canonical.

### Arithmetic and invariants
- Use checked math (checked_add/sub/mul/div).
- Avoid unchecked casts.
- Re-validate state after CPIs when required.

### State lifecycle
- Close accounts intentionally and securely.
- Avoid leaving "zombie" accounts with lamports.
- Ensure upgrades/ownership transfers are gated.

## Client-side checklist
- Cluster awareness: never hardcode mainnet endpoints in dev flows.
- Simulate transactions for UX where feasible.
- Handle blockhash expiry and retry with fresh blockhash when appropriate.
- Treat "signature received" as not-final; track confirmation.
- Never assume token program variant; detect or configure Token-2022 vs classic.
