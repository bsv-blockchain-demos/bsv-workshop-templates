---
title: "SPV proofs and verification"
description: "Simplified payment verification using Merkle proofs and block headers"
status: "Draft"
last_updated: ""
primitive_category: "Verification"
audience: "Advanced"
---

# SPV proofs and verification primitive module

## Learning objectives

- Understand how SPV enables lightweight transaction verification without full blockchain data.
- Learn to construct and verify Merkle proofs for transaction inclusion.
- Implement block header verification and proof-of-work validation.
- Build applications that can verify payments without running a full node.

## Summary

Learn how to implement simplified payment verification (SPV) using Merkle proofs and block headers. Participants will explore how to verify transaction inclusion in blocks and validate payments without downloading the entire blockchain.

## Core concept

SPV allows verification of transactions without storing the complete blockchain by using Merkle proofs to confirm transaction inclusion in blocks and validating block headers to ensure proof-of-work requirements are met.

## How it works on the BSV blockchain

- **Transaction structure**: standard transactions with additional Merkle proof data
- **Script requirements**: no special script requirements; verification happens off-chain
- **Data format**: Merkle proof consists of hash path and block header information
- **Validation**: cryptographic verification of Merkle tree inclusion and block validity

## Practical implementation

The SPV workflow involves requesting Merkle proofs from SPV servers, verifying transaction inclusion using cryptographic hashing, and validating block headers for proof-of-work compliance.

### Basic workflow

1. Request Merkle proof for a specific transaction
2. Verify transaction inclusion using Merkle tree path
3. Validate block header and proof-of-work
4. Confirm transaction is in a valid, confirmed block

### Code example

```js
// Minimal example showing SPV verification
async function verifySPVTransaction(txid, merkleProof, blockHeader) {
    // Step 1: Verify Merkle proof path
    const merkleRoot = calculateMerkleRoot(txid, merkleProof.path);
    // Step 2: Check block header contains this Merkle root
    if (blockHeader.merkleRoot !== merkleRoot) {
        throw new Error(‘Transaction not included in block’);
        }
    // Step 3: Verify block header proof-of-work
    const isValidPOW = verifyProofOfWork(blockHeader);
    if (!isValidPOW) {
        throw new Error(‘Invalid block proof-of-work’);
        }
    return {
        verified: true,
        blockHeight: blockHeader.height,
        blockHash: blockHeader.hash
        };
    }
```

## Common use cases

- Lightweight wallet applications that don't store full blockchain
- Mobile applications with limited storage and bandwidth
- Third-party verification services for payment confirmation
- IoT devices requiring transaction verification with minimal resources

## Current state and maturity

- **Implementation status**: Well-established protocol with multiple implementations
- **Available tools**: SPV libraries and services available for major programming languages
- **Known limitations**: Requires trusted SPV servers; vulnerable to certain network attacks

## Demo outline

Interactive web application demonstrating SPV verification of transactions without full blockchain data.

### Demo objectives

- Participants will verify transactions using only Merkle proofs and block headers
- They will understand how SPV reduces data requirements compared to full nodes
- They will implement basic SPV client functionality

### Demo steps

1. Setup: connect to SPV service provider
2. Request: obtain Merkle proof for a specific transaction
3. Verify: validate transaction inclusion using cryptographic proofs
4. Validate: check block header and proof-of-work
5. Confirm: display verification results and block information

## Practical exercises

- Request and verify a Merkle proof for a known transaction
- Implement Merkle root calculation from transaction hash and proof path
- Verify block header proof-of-work for a given block
- Build a simple SPV client that can verify payments
- Compare data requirements between SPV and full node verification

## Troubleshooting

- **Proof verification failures**: check Merkle proof path and transaction hash accuracy
- **Block header validation errors**: verify proof-of-work calculation and difficulty target
- **SPV server connectivity issues**: implement fallback servers and error handling

## What this module covers

- SPV protocol implementation and Merkle proof verification
- Block header validation and proof-of-work checking
- Lightweight verification patterns for resource-constrained environments

## What this module does not cover

- Full node implementation or complete blockchain validation
- Advanced SPV security considerations or attack mitigation
- Complex multi-signature or script verification beyond basic payment validation

## References and further reading

- SPV protocol specification in the original Bitcoin whitepaper
- Merkle tree construction and verification algorithms
- BSV block header format and proof-of-work requirements
