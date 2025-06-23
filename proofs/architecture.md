# Architecture Overview

## TORUS Warp Route Structure

TORUS is a Hyperlane Warp Route, which is a sophisticated cross-chain token that enables secure bridging between different networks. In this case, it bridges between Layer 1 and Base.

```
┌─────────────────┐         ┌─────────────────┐
│   L1 (Origin)   │         │  Base (Synthetic)│
│                 │         │                 │
│ Original TORUS  │◄────────┤  Proxy Contract │
│   Token         │  Bridge │                 │
│                 │         │  Implementation │
└─────────────────┘         └─────────────────┘
        │                           │
        │                           │
   ┌─────▼─────┐                ┌───▼───┐
   │ Hyperlane │                │ SAFE  │
   │Validators │                │Multisig│
   └───────────┘                └───────┘
```

## How It Works

**Proxy Pattern**: TORUS uses OpenZeppelin's transparent upgradeable proxy pattern. The proxy contract at `0x78ec15c5fd8efc5e924e9eebb9e549e29c785867` delegates all calls to the implementation contract at `0x8bf83DD46765CaB32614d6c8D0838276e908F753`.

**Implementation Contract**: Contains all the actual logic - ERC20 functions, bridge functions, and admin functions. The admin functions are now permanently disabled because the owner has been renounced.

**Proxy Admin**: Normally controls upgrades, but has been renounced to `0x000...000`, making upgrades impossible.

## Cross-Chain Bridge Mechanism

When you want to move TORUS from L1 to Base:

1. User deposits original TORUS on L1
2. L1 contract locks the tokens
3. Hyperlane validators observe and verify the deposit
4. Validators reach consensus on the cross-chain message
5. Message is delivered to Base
6. Base contract mints synthetic TORUS 1:1
7. User receives TORUS on Base

The reverse process burns synthetic tokens on Base and unlocks original tokens on L1.

## Security Model

**Hyperlane Validators**: The bridge is secured by multiple independent validators who must reach consensus. No single entity controls the bridge operations.

**Economic Security**: Validators stake significant value and lose it if they act maliciously or incorrectly.

**Proven Infrastructure**: The same validator network secures over $1B in cross-chain value for major protocols like Uniswap and Aave.

## What Makes This Different

Unlike a standard token, TORUS has multiple layers of security:

**Standard ERC20 Layer**: Normal transfer, approve, and balance functions work as expected.

**Bridge Layer**: Managed by Hyperlane's decentralized infrastructure, not by any single party.

**Governance Layer**: Token owner is a SAFE multisig, but with very limited powers since admin functions are renounced.

## Current Function Status

```solidity
// These work normally
function transfer(address to, uint256 amount) public returns (bool)
function approve(address spender, uint256 amount) public returns (bool)
function balanceOf(address account) public view returns (uint256)

// These are used by the bridge (internal functions)
function _mint(address account, uint256 amount) internal
function _burn(address account, uint256 amount) internal

// These are permanently disabled (owner renounced)
function mint(address to, uint256 amount) external onlyOwner  // DISABLED
function pause() external onlyOwner                          // DISABLED
function setFeeRate(uint256 rate) external onlyOwner         // DISABLED
```

## Comparison with Standard Tokens

| Feature | Standard Token | TORUS Warp Route |
|---------|---------------|------------------|
| Minting | Owner controlled | Bridge controlled only |
| Upgradeability | Owner can upgrade | Permanently locked |
| Pausing | Owner can pause | Permanently disabled |
| Cross-Chain | Not supported | Native bridge support |
| Governance | Single owner | Decentralized multisig |

## Multichain Expansion

The SAFE multisig can deploy TORUS to additional chains by:

1. Deploying the same implementation contract on the new chain
2. Configuring the Hyperlane bridge connection
3. Adding the new chain to the Hyperlane registry
4. Enabling cross-chain transfers

This allows TORUS to expand to any chain supported by Hyperlane while maintaining the same security guarantees and renounced admin functions.

## Technical Standards

**ERC20**: Standard token interface for compatibility with all wallets and DeFi protocols.

**EIP-1967**: Transparent proxy standard for predictable storage slots.

**OpenZeppelin**: Battle-tested contract implementations used by thousands of projects.

**Hyperlane**: Cross-chain infrastructure used by major protocols across the ecosystem.