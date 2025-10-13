---
title: "Payments on BSV blockchain"
description: "Learn how to send and receive payments on the BSV blockchain"
status: "Draft"
last_updated: ""
primitive_category: "Payments"
audience: "Beginner to Intermediate"
---

# Payments on BSV blockchain primitive module

## Learning objectives

- Understand the UTXO model and how balance is calculated.
- Send and receive BSV payments using a simple web application.
- Build and sign a basic transaction programmatically.
- Get familiar with fees, confirmations, and potential pitfalls.

## Summary

Learn how to send and receive payments on the BSV blockchain through a simple, interactive application. Participants will first experience payments from a user perspective and then explore how it works under the hood.

## Core concept

BSV payments work through the unspent transaction output (UTXO) model. Instead of account balances, the system tracks individual transaction outputs that can be spent as inputs to new transactions.

## How it works on the BSV blockchain

- **Transaction structure**: transactions consume previous outputs (inputs) and create new outputs, transferring value between addresses.
- **Script requirements**: basic payment transactions use standard pay-to-public-key-hash (P2PKH) scripts.
- **Data format**: transactions include inputs, outputs, fees, and digital signatures proving ownership.
- **Validation**: the network validates transactions by checking signatures, input availability, and fee adequacy.

## Practical implementation

The basic payment workflow involves listing available UTXOs, building a transaction, signing it with private keys, and broadcasting to the network.

### Basic workflow

1. List UTXOs to calculate available balance
2. Build transaction with inputs, outputs, and appropriate fees
3. Sign transaction with private keys
4. Broadcast transaction to the network and monitor for confirmation

### Code example

```js
// Minimal example showing the core implementation
async function sendPayment(fromAddress, toAddress, amount, privateKey) {
  // Step 1: Get UTXOs for the sender
  const utxos = await getUTXOs(fromAddress);
  // Step 2: Build transaction
  const transaction = buildTransaction(utxos, toAddress, amount);
  // Step 3: Sign transaction
  const signedTx = signTransaction(transaction, privateKey);
  // Step 4: Broadcast
  return broadcastTransaction(signedTx);
}
```

## Common use cases

- Peer-to-peer payments without intermediaries
- Micropayments for digital content or services
- Automated payments through programmatic interfaces

## Current state and maturity

- **Implementation status**: Production-ready with established standards
- **Available tools**: Multiple SDKs available in JavaScript, Python, and other languages
- **Known limitations**: Transaction fees vary with network conditions

## Demo outline

Interactive web application demonstrating the complete payment flow from a user perspective.

### Demo objectives

- Participants will send and receive BSV payments
- They will understand how balance calculation works with UTXOs
- They will observe transaction confirmation on the blockchain

### Demo steps

1. Setup: connect to a wallet or use provided test credentials
2. View balance: display current balance calculated from UTXOs
3. Send payment: enter recipient address and amount, sign and broadcast
4. Receive payment: show current address and QR code for receiving
5. Monitor: check transaction status and confirmations

## Practical exercises

- Implement getBalance() function using UTXO aggregation
- Create and broadcast a simple payment transaction
- Verify transaction appears in a block explorer
- Build a script to monitor for incoming transactions

## Troubleshooting

- **Insufficient funds**: verify balance accounts for transaction fees
- **Transaction not confirming**: check fee amount and mempool status
- **Invalid signature**: ensure correct private key and transaction format

## What this module covers

- Basic payment functionality using standard BSV transactions
- UTXO model fundamentals and balance calculation
- Transaction building, signing, and broadcasting workflows

## What this module does not cover

- Advanced script types or smart contract functionality
- Multi-signature transactions or complex spending conditions
- Production security practices for large-value transactions

## References and further reading

- BSV protocol specifications for transaction formats
- SDK documentation for supported programming languages
- Block explorer services for transaction verification
