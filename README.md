# SwapGuard Hook — Uniswap v4

SwapGuard is a learning/prototype Uniswap v4 Hook built with Solidity and Foundry.

It allows a pool owner/admin to configure a maximum swap amount for each pool. Swaps above the configured limit are rejected inside the `beforeSwap` hook.

> Educational prototype. Not audited and not production ready.

## Why I Built It

I am learning Web3 and Uniswap v4 by building real projects rather than only studying theory.

This project helped me learn:

- Uniswap v4 Hooks
- Solidity mappings
- Pool-specific state
- `beforeSwap`
- access control with `msg.sender`
- custom errors
- Solidity events
- Foundry testing
- positive and negative smart-contract tests

## How It Works

Each Uniswap pool can have its own maximum allowed swap amount.

Example:

```text
Pool A limit = 1 token

Swap 0.5 token → allowed
Swap 1 token   → allowed
Swap 2 tokens  → reverted

The owner configures the limit:
setMaxSwapAmount(poolId, 1e18);

Before a swap executes, the Hook checks the configured limit.
Conceptually:
User requests swap
        ↓
Uniswap calls beforeSwap()
        ↓
SwapGuard reads the pool limit
        ↓
Amount exceeds limit?
      /            \
    Yes             No
     ↓               ↓
  Revert          Continue swap

Core Logic
The pool-specific limits are stored using:
mapping(PoolId => uint256) public maxSwapAmount;

The Hook checks the current pool inside _beforeSwap().
If the requested amount exceeds the configured limit, the transaction reverts.
Access Control
Only the contract owner can update pool limits.
Unauthorized callers receive:
error NotOwner();

Events
When the maximum swap amount changes, the contract emits:
event MaxSwapAmountUpdated(
    uint256 oldAmount,
    uint256 newAmount
);

Testing
The project uses Foundry.
Run:
forge build
forge test

The tests cover:
- normal swaps
- swaps above the configured limit
- swaps at the limit
- owner configuration
- unauthorized configuration attempts
- event emission
- swap counters
- liquidity hook callbacks
Tech Stack:


- Solidity
- Foundry
- Uniswap v4
- OpenZeppelin Uniswap Hooks
- Git / GitHub
Repository Structure:


src/
  SwapGuardHook.sol

test/
  Counter.t.sol

Current Status:
Prototype / learning project.

This code has not been professionally audited and should not be used with real funds in production.

What I'm Working On
I am currently focused on:
- Solidity
- Foundry
- Uniswap v4 Hooks
- DeFi smart-contract development
- smart-contract testing
I'm also available for small prototype work involving:
- Uniswap v4 Hooks
- Solidity modifications
- Foundry tests
- contract debugging
- Web3 proof-of-concepts