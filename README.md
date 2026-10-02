# SwapGuard Hook — Uniswap v4

A learning/prototype Uniswap v4 Hook that allows pool-specific maximum
swap amounts.

## Features

- Pool-specific swap limits
- Owner-controlled configuration
- Rejects swaps above configured limits
- Emits configuration update events
- Tracks swap activity
- Tested using Foundry

## Example

Pool limit: 1 token

Swap 1 token → allowed
Swap 2 tokens → reverted

## Tech

- Solidity
- Foundry
- Uniswap v4
- OpenZeppelin Uniswap Hooks

## Status

Educational prototype. Not audited or production ready.