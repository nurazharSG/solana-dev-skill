# Programs with Anchor (default choice)

## When to use Anchor
Use Anchor by default when:
- you want fast iteration
- you want an IDL and a TS client story
- you want mature testing and workspace tooling

## Version management
- Use AVM (Anchor Version Manager) when you need reproducible builds or multiple Anchor versions.
- Keep Solana CLI + Anchor versions aligned in CI and developer setup.

## Program design best practices
- Minimize trust in instruction inputs: all accounts are attacker-controlled.
- Use account constraints where possible (ownership checks, seeds, has_one, signer, mut).
- Use PDAs for program-owned state; ensure seeds/bump are validated and consistent.
- Explicitly validate token program and mint/account relationships, especially with Token-2022 and extensions.

## CPI best practices
- Validate every account you pass to a CPI.
- Do not allow arbitrary CPI target programs unless explicitly intended.
- Do not pass extra writable/signing privileges to the callee.
- Prefer explicit program IDs for known CPIs (system program, token program, metadata program, etc).

## IDL and clients
- Treat the program's IDL as a product artifact.
- Prefer generating clients (Codama) when you want Kit-native clients.
- If you must use Anchor TS client in a Kit-first app, put it behind the web3-compat boundary.

## Testing
- Use `anchor test` for end-to-end tests where it's valuable.
- Prefer Bankrun-based tests for fast iteration when the scenario fits.
- If you use Anchor + Bankrun, consider anchor-bankrun patterns to reduce friction.

## Anchor-specific gotchas to watch for
- Legacy IDL formats (pre-0.30) vs new IDL spec: ensure tooling agrees on the format.
- Serialization mismatches: keep crates and TS packages aligned.
- PDA seeds: ensure all seed material is stable and canonical (byte order, string encoding, etc).
