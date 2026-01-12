# Testing strategy (Bankrun / Surfpool / test-validator)

## Default testing pyramid
1) Unit tests (fast): Bankrun
2) Integration tests (realistic state): Surfpool
3) Cluster smoke tests: devnet/testnet/mainnet as needed

## Bankrun
Use Bankrun when:
- you want fast iteration
- you don't need full RPC node behavior
- you want advanced test controls (time travel, account manipulation)

Use solana-test-validator instead when:
- you need RPC methods or validator behaviors that bankrun doesn't emulate

## Surfpool
Use Surfpool when:
- your program or client relies on CPI into complex mainnet programs
- you want realistic accounts/programs available locally without manually dumping them

Basic usage:
- `surfpool start`
- Use Surfpool Studio UI to inspect transactions, accounts, and run local faucet actions.

## Suggested test layout
- `tests/unit/*.test.ts` (bankrun)
- `tests/integration/*.test.ts` (surfpool or test-validator)
- Keep fixtures minimal; prefer deterministic PDAs and seeded keypairs for reproducibility.

## CI guidance
- Keep bankrun tests as the default CI gate (fast).
- Run integration tests in a separate job/stage to control runtime and external dependencies.
