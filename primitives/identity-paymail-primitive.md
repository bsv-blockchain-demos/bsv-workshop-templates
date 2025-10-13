---
title: "Identity and Paymail addressing"
description: "Human-readable addresses and identity verification using Paymail protocol"
status: "Draft"
last_updated: ""
primitive_category: "Identity"
audience: "Intermediate"
---

# Identity and Paymail addressing primitive module

## Learning objectives

- Understand how Paymail provides human-readable addresses for BSV payments.
- Implement Paymail address resolution to BSV addresses.
- Learn identity verification patterns using Paymail.
- Build applications that use email-like addressing for payments.

## Summary

Learn how to use Paymail for human-readable addressing and identity verification on the BSV blockchain. Participants will explore how to resolve Paymail addresses, send payments using email-like identifiers, and implement identity verification workflows.

## Core concept

Paymail provides email-like addresses (user@domain.com) that resolve to BSV addresses, making payments more user-friendly while enabling identity verification and additional services through the underlying protocol.

## How it works on the BSV blockchain

- **Transaction structure**: standard BSV payments with Paymail address resolution
- **Script requirements**: standard P2PKH transactions after address resolution
- **Data format**: Paymail addresses resolved through DNS and HTTPS protocols
- **Validation**: address resolution verified through cryptographic signatures

## Practical implementation

The Paymail workflow involves address resolution through DNS/HTTPS, payment destination lookup, and optional identity verification through the Paymail protocol.

### Basic workflow

1. Parse Paymail address format (user@domain.com)
2. Resolve Paymail to BSV address via DNS/HTTPS
3. Send payment to resolved BSV address
4. Optional: verify identity through Paymail protocol

### Code example

```js
// Minimal example showing Paymail resolution
async function sendToPaymail(paymailAddress, amount, privateKey) {
    // Step 1: Validate Paymail format
    if (!isValidPaymailFormat(paymailAddress)) {
        throw new Error(‘Invalid Paymail format’);
        }
    // Step 2: Resolve Paymail to BSV address
    const bsvAddress = await resolvePaymailAddress(paymailAddress);
    // Step 3: Send payment to resolved address
    const transaction = buildTransaction(bsvAddress, amount);
    const signed = signTransaction(transaction, privateKey);
    return broadcastTransaction(signed);
    }
```

## Common use cases

- User-friendly payment addresses for applications
- Identity verification for business transactions
- Email-like addressing for recurring payments
- Integration with existing business systems using email identifiers

## Current state and maturity

- **Implementation status**: Established protocol with multiple implementations
- **Available tools**: Paymail libraries available in multiple programming languages
- **Known limitations**: Requires DNS/HTTPS infrastructure; not all wallets support Paymail

## Demo outline

Interactive web application demonstrating Paymail address resolution and payment workflows.

### Demo objectives

- Participants will send payments using Paymail addresses
- They will understand the resolution process from email-like addresses to BSV addresses
- They will see identity verification capabilities

### Demo steps

1. Setup: connect to wallet and configure Paymail-capable environment
2. Resolve: enter Paymail address and show resolved BSV address
3. Pay: send payment using Paymail address instead of BSV address
4. Verify: demonstrate identity verification through Paymail protocol
5. Receive: show how to receive payments at a Paymail address

## Practical exercises

- Implement Paymail address validation and parsing
- Resolve a Paymail address to its corresponding BSV address
- Send a payment using a Paymail address
- Set up basic Paymail receiving capability
- Implement identity verification using Paymail signatures

## Troubleshooting

- **Resolution failures**: verify DNS configuration and HTTPS endpoints
- **Invalid Paymail format**: check address format against specification
- **Payment delivery issues**: confirm resolved BSV address is correct and accessible

## What this module covers

- Paymail protocol implementation for address resolution
- Human-readable addressing for improved user experience
- Basic identity verification patterns using Paymail

## What this module does not cover

- Advanced Paymail features like payment requests or invoicing
- Complex identity verification or KYC integration
- DNS server configuration for hosting Paymail services

## References and further reading

- Paymail protocol specification and documentation
- DNS and HTTPS configuration requirements for Paymail hosting
- Identity verification best practices for blockchain applications
