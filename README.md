# Cobo TSS Node Release

Pre-built binaries for [Cobo TSS Node](https://www.cobo.com/mpc-wallet) — the client-side component for Cobo's MPC co-managed custody solution.

## Download

Download the latest release from the [Releases](https://github.com/CoboGlobal/cobo-tss-node-release/releases) page.

### Available Platforms

| Platform | Architecture | Filename |
|----------|-------------|----------|
| Linux | x86_64 (amd64) | `cobo-tss-node-<version>-linux-amd64.tar.gz` |
| Linux | ARM64 | `cobo-tss-node-<version>-linux-arm64.tar.gz` |
| macOS | Intel (amd64) | `cobo-tss-node-<version>-darwin-amd64.tar.gz` |
| macOS | Apple Silicon (arm64) | `cobo-tss-node-<version>-darwin-arm64.tar.gz` |

## Quick Start

```bash
# Download and extract (example: Linux amd64)
tar xzf cobo-tss-node-v0.12.0-linux-amd64.tar.gz
cd cobo-tss-node-v0.12.0-linux-amd64

# Initialize node
./cobo-tss-node init

# View node info (save your TSS Node ID)
./cobo-tss-node info

# Start node
./cobo-tss-node start --prod
```

## What's Inside

Each archive contains:

```
cobo-tss-node-<version>-<os>-<arch>/
├── cobo-tss-node                              # Main binary
├── SHA256SUMS                                 # Checksums for verification
└── configs/
    └── cobo-tss-node-config.yaml.template     # Configuration template
```

## Verify Integrity

```bash
cd cobo-tss-node-<version>-<os>-<arch>
sha256sum -c SHA256SUMS
```

## CLI Reference

| Command | Description |
|---------|-------------|
| `init` | Initialize TSS Node keys and encrypted database |
| `start` | Start the TSS Node service |
| `info` | Display Node ID and metadata |
| `info group [id]` | List/inspect MPC groups |
| `sign` | Sign a message for periodic key share checkup |
| `export-share` | Export encrypted key shares for disaster recovery |
| `change-password` | Change database encryption password |
| `migrate` | Run database schema migration |
| `event key create/info` | Manage event publishing keys |
| `version` | Show version information |

### Global Flags

```
-c, --config string      Config file path (default: configs/cobo-tss-node-config.yaml)
-d, --db string          Database file path (default: db/secrets.db)
    --key-file string    Database encryption key file (for non-interactive use)
    --password-segment   Enable password segment input
```

### Environment Modes

```bash
./cobo-tss-node start --dev      # Development
./cobo-tss-node start --sandbox  # Sandbox (testing)
./cobo-tss-node start --prod     # Production
```

## Security

- Database is AES-GCM encrypted; password required on every operation
- Use `--key-file` for automated/service deployments (file must be mode `600`)
- Supports callback-based risk control for transaction approval
- Built-in embedded risk control rules for keygen/keysign/reshare

## Related

- [cobo-tss-node-skill](https://github.com/CoboTest/cobo-tss-node-skill) — Automation scripts for install, service setup, and daily operations
- [Cobo MPC Wallet Documentation](https://www.cobo.com/developers/mpc-wallet)

## License

Proprietary — Cobo © 2026
