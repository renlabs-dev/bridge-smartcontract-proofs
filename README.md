# TORUS Token - Decentralization & Security Proofs

**Contract Address:** `0x78ec15c5fd8efc5e924e9eebb9e549e29c785867` (Base Network)


### Verification Status

**The contract IS verified on BaseScan:** https://basescan.org/address/0x78ec15c5fd8efc5e924e9eebb9e549e29c785867#code

**Owners CANNOT modify behaviour because:**
- Proxy admin ownership: **RENOUNCED** (0x000...000)
- Implementation ownership: **RENOUNCED** (0x000...000)  
- All admin functions: **PERMANENTLY DISABLED**

## What TORUS Actually Is

TORUS is a Hyperlane Warp Route, which is a synthetic token that bridges between L1 and Base. It uses Hyperlane's battle-tested bridge infrastructure that secures over $1B in value across major protocols.

**Key Points:**
- Listed in official Hyperlane registry: https://github.com/hyperlane-xyz/hyperlane-registry/tree/main/chains/torus
- Uses transparent upgradeable proxy pattern (standard OpenZeppelin)
- All administrative control permanently renounced
- Token owner is a SAFE multisig (only for multichain expansion)

## Current Status Summary

| Component | Address | Status |
|-----------|---------|--------|
| Token Contract | `0x78ec15c5fd8efc5e924e9eebb9e549e29c785867` | Verified |
| Implementation | `0x8bf83DD46765CaB32614d6c8D0838276e908F753` | Owner Renounced |
| Proxy Admin | `0x9925cdbea5b91542bba6e1fc967465b1c1ed7156` | Renounced |
| Token Owner | `0x9b23a261fa354a6f8758fcc44656df6f317db4dc` | SAFE Multisig |

## Security Guarantees

**What Cannot Happen:**
- No minting (implementation owner renounced)
- No pausing (implementation owner renounced)  
- No fee changes (implementation owner renounced)
- No upgrades (proxy admin renounced)
- No rug pulls (all control mechanisms disabled, liquidity locked)

**What Can Happen:**
- Standard ERC20 transfers
- Cross-chain bridging via Hyperlane
- Deployment to new chains (SAFE multisig controlled)

## Detailed Proofs

**[Hyperlane Registry Proof](./proofs/hyperlane-registry.md)** - Official listing in Hyperlane's public registry

**[Contract Ownership Proofs](./proofs/ownership-renunciation.md)** - Step-by-step verification of complete renunciation

**[Architecture Overview](./proofs/architecture.md)** - Technical structure and warp route mechanics

**[Liquidity Analysis](./proofs/liquidity.md)** - LP security and locking status
