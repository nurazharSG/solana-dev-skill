# Solana Development Skill for Claude Code

A comprehensive Claude Code skill for modern Solana development (January 2026 best practices).

## Overview

This skill provides Claude Code with deep knowledge of the current Solana development ecosystem:

- **UI**: Solana Foundation framework-kit (`@solana/client` + `@solana/react-hooks`)
- **SDK**: `@solana/kit` (v5.x) for new client work
- **Legacy Interop**: `@solana/web3-compat` for bridging to web3.js dependencies
- **Programs**: Anchor (default), Pinocchio/Steel for specialized needs
- **Testing**: Bankrun for unit tests, Surfpool for integration
- **Codegen**: Codama-first IDL and client generation

## Installation

### Quick Install (Personal)

```bash
# Clone and install to personal skills directory
git clone https://github.com/YOUR_USERNAME/solana-dev-skill.git
cp -r solana-dev-skill/skill ~/.claude/skills/solana-dev
```

### Quick Install (Project)

```bash
# Install to project-specific skills directory
cp -r solana-dev-skill/skill .claude/skills/solana-dev
```

### Using the Install Script

```bash
# Install to personal directory (default)
./install.sh

# Install to project directory
./install.sh --project

# Install to custom location
./install.sh --path /custom/path/skills/solana-dev
```

## Skill Structure

```
skill/
├── SKILL.md                    # Main skill definition (required)
├── frontend-framework-kit.md   # UI patterns with framework-kit
├── kit-web3-interop.md         # Kit ↔ web3.js boundary patterns
├── programs-anchor.md          # Anchor program development
├── programs-native.md          # Native programs (Pinocchio/Steel)
├── testing.md                  # Testing strategy (Bankrun/Surfpool)
├── idl-codegen.md              # IDL and client generation
├── payments.md                 # Payments and commerce
├── security.md                 # Security checklist
└── resources.md                # Curated reference links
```

## Usage

Once installed, Claude Code will automatically use this skill when you ask about:

- Solana dApp UI work (React / Next.js)
- Wallet connection and signing flows
- Transaction building, sending, and confirmation UX
- On-chain program development (Anchor or native Rust)
- Client SDK generation (typed program clients)
- Local testing (Bankrun, Surfpool, test-validator)
- Security hardening and audit-style reviews

### Example Prompts

```
"Help me set up a Next.js app with Solana wallet connection"
"Create an Anchor program for a simple escrow"
"How do I integrate a legacy web3.js library with my Kit-based app?"
"Write Bankrun tests for my token transfer instruction"
"Review this program for security issues"
```

## Stack Decisions

This skill encodes opinionated best practices:

| Layer | Default Choice | Alternative |
|-------|---------------|-------------|
| UI Framework | framework-kit | ConnectorKit (headless) |
| Client SDK | @solana/kit | @solana/web3-compat (boundary) |
| Program Framework | Anchor | Pinocchio, Steel |
| Unit Testing | Bankrun | solana-program-test |
| Integration Testing | Surfpool | solana-test-validator |
| Client Generation | Codama | Kinobi (Umi) |

## Progressive Disclosure

The skill uses Claude Code's progressive disclosure pattern. The main `SKILL.md` provides core guidance, and Claude reads the specialized markdown files only when needed for specific tasks.

## Contributing

Contributions are welcome! Please ensure any updates reflect current Solana ecosystem best practices.

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) for details.

## Resources

- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Claude Code Skills Guide](https://code.claude.com/docs/en/skills)
- [Solana Documentation](https://solana.com/docs)
- [framework-kit Repository](https://github.com/solana-foundation/framework-kit)
- [@solana/kit Repository](https://github.com/anza-xyz/kit)
