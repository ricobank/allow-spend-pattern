
`allow(uint256 amount)` - allocate `amount` tokens from the caller to the transaction
`spend(uint256 amount)` - move `amount` tokens from the transaction to the caller

This document describes a token pattern which is currently not possible to implement in full, but has a lot of interesting and useful properties.
The most straightforward way to implement it would be using a `TXID` opcode.

The basic idea is that instead of pushing and pulling tokens to each other, contracts transiently push and pull tokens *into the transaction*.
You can think of these as flash loan without an external contract calls.

The trick is to keep track of the implied refund on a per-allower basis. Next time the balance is accessed, process the refund first.