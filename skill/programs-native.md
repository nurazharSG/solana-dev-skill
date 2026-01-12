# Native programs (Pinocchio / Steel)

## When to consider native frameworks
Use native approaches when you explicitly need:
- extreme control over compute usage and binary size
- fewer dependencies / less dependency hell
- custom parsing and zero-copy flows
- no_std requirements

## Pinocchio
- Goal: zero external dependencies (beyond Solana SDK types), optimized for CU and binary size.
- Pattern: parse instruction inputs as bytes, use zero-copy techniques, avoid allocations.

Use when:
- performance and footprint are a primary requirement
- you can afford more manual work and stricter invariants

## Steel
- Goal: a lightweight, modular framework for native Solana programs with helper patterns.
- Warning: under active development; interfaces may change; code may be unaudited.

Use when:
- you want a less opinionated alternative to Anchor but still want structure and helpers
- you can tolerate API churn and take responsibility for audits/testing

## Interop with IDLs
- For native programs, plan your IDL strategy early:
  - Shank macros to extract IDL
  - Convert to Codama to generate clients

## Testing
- For native programs, use solana-program-test style tests where appropriate.
- For integration-like tests, Surfpool is often a better dev loop than dumping mainnet state manually.
