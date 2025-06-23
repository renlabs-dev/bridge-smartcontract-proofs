# Contract Ownership Proofs

## Complete Administrative Renunciation

All administrative control over TORUS has been permanently renounced. 

## Proxy Admin Renunciation

**Address:** `0x9925cdbea5b91542bba6e1fc967465b1c1ed7156`

Visit the proxy admin contract on BaseScan: https://basescan.org/address/0x9925cdbea5b91542bba6e1fc967465b1c1ed7156

Check the owner() function. It returns `0x0000000000000000000000000000000000000000`.

This means the proxy admin has been renounced to the zero address. No one can:
- Upgrade the implementation contract
- Change the proxy admin
- Modify proxy behavior in any way

## Implementation Owner Renunciation  

**Address:** `0x8bf83DD46765CaB32614d6c8D0838276e908F753`

Visit the implementation contract: https://basescan.org/readContract?a=0x8bf83DD46765CaB32614d6c8D0838276e908F753&v=0x8bf83DD46765CaB32614d6c8D0838276e908F753#readCollapse7

Read the owner() function. It also returns `0x0000000000000000000000000000000000000000`.

With the implementation owner renounced, these functions are permanently disabled:

```solidity
function mint(address to, uint256 amount) onlyOwner  // DISABLED
function pause() onlyOwner                          // DISABLED  
function unpause() onlyOwner                        // DISABLED
function setFeeRate(uint256 newRate) onlyOwner      // DISABLED
```

The functions exist in the code but cannot be called because there's no owner.

## Current Token Owner

**Address:** `0x9b23a261fa354a6f8758fcc44656df6f317db4dc` (SAFE Multisig)

The token itself still has an owner, but this owner can only:
- Deploy the token to new chains (multichain expansion)
- Perform standard ERC20 operations

The token owner CANNOT:
- Mint new tokens (implementation owner renounced)
- Pause the contract (implementation owner renounced)
- Upgrade the logic (proxy admin renounced)
- Change fees (implementation owner renounced)

The SAFE multisig provides additional security through multi-signature requirements and transparent on-chain operations.

## Attack Vectors Eliminated

With ownership renounced, these common rug pull methods are impossible:

**Minting Tokens** - Cannot be done, owner is zero address
**Pausing Trading** - Cannot be done, owner is zero address  
**Upgrading to Malicious Code** - Cannot be done, admin is zero address
**Changing Fees** - Cannot be done, owner is zero address

The only functions that remain are standard ERC20 operations and bridge functionality managed by Hyperlane's decentralized infrastructure.

This level of renunciation goes beyond what most projects do and provides mathematical proof that the token cannot be rugpulled through administrative functions. 