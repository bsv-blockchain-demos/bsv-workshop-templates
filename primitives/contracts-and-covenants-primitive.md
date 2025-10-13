---
title: "Contracts and covenants"
description: "Programmable spending conditions using Bitcoin Script and covenant patterns"
status: "Draft"
last_updated: ""
primitive_category: "Smart Contracts"
audience: "Advanced"
---

# Contracts and covenants primitive module

## Learning objectives

- Understand Bitcoin Script and programmable spending conditions.
- Learn about covenant patterns that constrain future transactions.
- Implement basic smart contracts using script templates.
- Build applications that enforce specific transaction rules automatically.

## Summary

Learn how to create programmable spending conditions using Bitcoin Script and covenant patterns. Participants will explore how to build smart contracts that enforce rules about how funds can be spent in future transactions.

## Core concept

Smart contracts on BSV use Bitcoin Script to define spending conditions. Covenants are scripts that constrain how outputs can be spent in future transactions, enabling complex automated agreements and programmable money flows.

## How it works on the BSV blockchain

- **Transaction structure**: outputs include custom scripts defining spending conditions
- **Script requirements**: uses Bitcoin Script opcodes to implement contract logic
- **Data format**: contract state stored in transaction outputs and script data
- **Validation**: contract execution verified by script interpretation during transaction validation

## Practical implementation

The contract workflow involves designing spending conditions, implementing them in Bitcoin Script, creating transactions with contract outputs, and executing contracts through subsequent spending transactions.

### Basic workflow

1. Design contract logic and spending conditions
2. Implement contract using Bitcoin Script templates
3. Create transaction with contract output
4. Execute contract by creating valid spending transaction

### Code example

```js
// Minimal example showing basic contract implementation
function createTimelockContract(unlockTime, recipientAddress) {
    // Contract that releases funds after specified time
    const script = `${unlockTime} OP_CHECKLOCKTIMEVERIFY OP_DROP OP_DUP OP_HASH160 ${hash160(recipientAddress)}  OP_EQUALVERIFY OP_CHECKSIG`;
    return compileScript(script);
}
function spendTimelockContract(contractUtxo, recipientPrivateKey, currentTime) {
    if (currentTime < contractUtxo.unlockTime) {
        throw new Error(‘Contract timelock not yet expired’);
        }
    const spendingTx = buildSpendingTransaction(contractUtxo, recipientPrivateKey);
    return spendingTx;
    }
```

## Common use cases

- Escrow services with automated release conditions
- Multi-signature wallets requiring multiple approvals
- Time-locked payments that release at specific dates
- Conditional payments based on external data verification

## Current state and maturity

- **Implementation status**: Core Bitcoin Script functionality is mature and tested
- **Available tools**: Script templates and libraries available for common patterns
- **Known limitations**: Script complexity affects transaction fees; some advanced opcodes disabled

## Demo outline

Interactive web application demonstrating contract creation and execution workflows.

### Demo objectives

- Participants will create simple smart contracts with spending conditions
- They will execute contracts by providing valid spending proofs
- They will understand how contract logic constrains future transactions

### Demo steps

1. Setup: prepare development environment with script tools
2. Design: create contract logic for specific use case
3. Deploy: create transaction with contract output
4. Execute: spend contract by satisfying spending conditions
5. Verify: confirm contract execution on blockchain

## Practical exercises

- Create a timelock contract that releases funds after a specific block height
- Implement a multi-signature contract requiring 2-of-3 signatures
- Build a hash-lock contract that requires knowledge of a secret
- Design a covenant that enforces specific output formats in spending transactions
- Test contract execution and verify proper constraint enforcement

## Troubleshooting

- **Script execution failures**: verify script syntax and opcode usage
- **Contract spending issues**: ensure spending transaction satisfies all contract conditions
- **Fee calculation errors**: account for increased script complexity in fee estimation

## What this module covers

- Bitcoin Script fundamentals and common contract patterns
- Covenant design and implementation techniques
- Contract testing and deployment workflows

## What this module does not cover

- Advanced cryptographic protocols or zero-knowledge proofs
- Complex multi-party contract protocols
- Production security analysis or formal verification methods

## References and further reading

- Bitcoin Script reference and opcode documentation
- Covenant pattern libraries and implementation examples
- Smart contract security best practices for production deployment
