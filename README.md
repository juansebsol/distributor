# merkle-distributor

A program for distributing tokens efficiently via uploading a [Merkle root](https://en.wikipedia.org/wiki/Merkle_tree).

## Recent Updates (2024-09-29)

This project has been successfully migrated to the latest Solana and Anchor versions for improved performance, security, and compatibility.

### Migration Summary

**What was updated:**
- **Anchor Framework**: 0.28.0 to 0.31.1
- **Solana SDK**: 1.16.16 to 2.2.17 (Agave)
- **Rust Toolchain**: 1.72.0 to 1.90.0
- **SPL Token**: 2.2.0 to 3.0.0

**Key Changes:**
- Updated all dependencies to latest compatible versions
- Migrated from direct `solana_program` imports to `anchor_lang::solana_program`
- Fixed API changes in Anchor 0.31.1 (bumps.get() → bumps.distributor)
- Added `idl-build` feature for proper IDL generation
- Updated Rust to support 2024 edition dependencies
- Successfully deployed to Solana devnet

**Deployment Details:**
- **Program ID**: `AnZmMDQ3b5c6LijNGGGtoD79ZTpoxmsPeDki3U18eVcV`
- **Network**: Devnet
- **Transaction**: `4uVw5zhTdYm8w55Wt4cTKkesbEx8pG27JHqJ6dKysFaLryMjf6iNYEb31syt3Qk1eLfoLqHnozWk8SGreHttJw1t`

### Breaking Changes

1. **Import Changes**: All `solana_program` imports now use `anchor_lang::solana_program`
2. **Bumps API**: Changed from `ctx.bumps.get("account")` to `ctx.bumps.account`
3. **Dependencies**: Removed direct `solana_program` dependencies (now provided by Anchor)

### Development Environment

**Required Versions:**
- Rust: 1.90.0+
- Solana CLI: 2.2.17+
- Anchor CLI: 0.31.1+

**Installation:**
```bash
# Update Rust
rustup update stable

# Install Solana CLI
sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)"

# Install Anchor CLI
cargo install --git https://github.com/coral-xyz/anchor avm --force
avm install 0.31.1
avm use 0.31.1
```

## Claiming Airdrop via CLI

To claim via CLI instead of using `https://jito.network/airdrop`, run the following commands.

1. Build the cli (must have rust + cargo installed):

```bash
cargo b -r
```

2. Run `claim` with the proper args. Be sure to replace `<YOUR KEYPAIR>` with the _full path_ of your keypair file. This will transfer tokens from the account `8Xm3tkQH581s3MoRHWUNYA5jKbgPATW4tJAAxgwDC6T6` to a the associated token account owned by your keypair, creating it if it doesn't exist.

```bash
./target/release/cli --rpc-url https://api.mainnet-beta.solana.com --keypair-path <YOUR KEYPAIR> --airdrop-version 0 --mint jtojtomepa8beP8AuQc6eXt5FriJwfFMwQx2v2f9mCL --program-id mERKcfxMC5SqJn4Ld4BUris3WKZZ1ojjWJ3A3J5CKxv claim --merkle-tree-path merkle_tree.json
```

Note that for searchers and validators, not all tokens will be vested until December 7, 2024. You can check the vesting status at `https://jito.network/airdrop`.

## Building and Deploying

### Build the Program
```bash
anchor build
```

### Deploy to Devnet
```bash
anchor deploy
```

### Deploy to Mainnet
```bash
# Switch to mainnet
solana config set --url https://api.mainnet-beta.solana.com

# Update Anchor.toml cluster to "mainnet"
# Update Anchor.toml wallet to your mainnet keypair

# Deploy
anchor deploy
```


## Key Features

- **Vesting System**: Implements time-locked token distribution
- **Merkle Proof Verification**: Secure, gas-efficient claiming
- **Clawback Mechanism**: Admin can reclaim unclaimed tokens
- **Frontrunning Protection**: Built-in security measures
- **Multi-Component Architecture**: Program, API, CLI, and utilities

## Troubleshooting

If you encounter issues:

1. **Rust Edition Errors**: Ensure you're using Rust 1.90.0+
2. **Dependency Conflicts**: Run `cargo clean` and rebuild
3. **Deployment Issues**: Verify your Solana CLI configuration matches Anchor.toml
4. **Build Errors**: Check that all versions match the requirements above
