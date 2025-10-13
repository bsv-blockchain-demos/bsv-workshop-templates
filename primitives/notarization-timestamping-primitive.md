---
title: "Notarization and timestamping"
description: "Cryptographic proof-of-existence and timestamping using blockchain immutability"
status: "Draft"
last_updated: ""
primitive_category: "Notarization"
audience: "Intermediate"
---

# Notarization and timestamping primitive module

## Learning objectives

- Understand how blockchain provides immutable timestamping for documents and data.
- Learn to create cryptographic proof-of-existence without revealing document contents.
- Implement document notarization workflows using hash-based verification.
- Build applications that provide verifiable timestamps for audit trails.

## Summary

Learn how to create cryptographic proof-of-existence and timestamping using the BSV blockchain's immutability. Participants will explore how to notarize documents and data without revealing their contents while providing verifiable timestamps for audit and compliance purposes.

## Core concept

Notarization on blockchain uses cryptographic hashing to prove a document existed at a specific time without revealing its contents. The hash is stored in a transaction, providing immutable proof that can be verified independently.

## How it works on the BSV blockchain

- **Transaction structure**: document hashes stored in OP_RETURN outputs with timestamp data
- **Script requirements**: uses OP_RETURN for data storage, no special script logic required
- **Data format**: SHA-256 hashes with optional metadata about document type or purpose
- **Validation**: proof verified by comparing document hash with stored hash and checking block timestamp

## Practical implementation

The notarization workflow involves hashing documents, storing hashes on-chain with metadata, and later providing verification by comparing original documents with stored hashes.

### Basic workflow

1. Hash document or data using SHA-256
2. Store hash on blockchain with timestamp and optional metadata
3. Provide proof by showing original document and transaction reference
4. Verify proof by hashing original and comparing with blockchain record

### Code example

```js
// Minimal example showing document notarization
async function notarizeDocument(documentData, metadata = {}) {
    // Step 1: Create document hash
    const documentHash = sha256(documentData);
    // Step 2: Prepare notarization data
    const notarizationData = {
        hash: documentHash,
        timestamp: Date.now(),
        type: metadata.type || ‘document’,
        description: metadata.description || ‘’
        };
    // Step 3: Store on blockchain
    const tx = buildNotarizationTransaction(notarizationData);
    const txid = await broadcastTransaction(tx);
        return {
        txid: txid,
        hash: documentHash,
        timestamp: notarizationData.timestamp
        };
    }
    async function verifyNotarization(originalDocument, txid) {
    const originalHash = sha256(originalDocument);
    const storedData = await getNotarizationData(txid);
        return {
        verified: originalHash === storedData.hash,
        timestamp: storedData.timestamp,
        blockTime: storedData.blockTime
        };
}
```

## Common use cases

- Legal document timestamping for compliance and audit trails
- Intellectual property protection and patent priority establishment
- Digital certificate and credential verification
- Supply chain documentation and provenance tracking

## Current state and maturity

- **Implementation status**: Well-established pattern with proven legal and technical validity
- **Available tools**: Multiple services and libraries support blockchain notarization
- **Known limitations**: Verification requires access to original document; legal recognition varies by jurisdiction

## Demo outline

Interactive web application demonstrating document notarization and verification workflows.

### Demo objectives

- Participants will notarize documents and data on the blockchain
- They will verify previously notarized documents using hash comparison
- They will understand the privacy and immutability benefits of hash-based notarization

### Demo steps

1. Setup: prepare document or data for notarization
2. Hash: compute SHA-256 hash and display result
3. Notarize: store hash on blockchain with timestamp
4. Record: save transaction ID for future verification
5. Verify: prove document authenticity using original and transaction reference

## Practical exercises

- Notarize a text document and verify it using the transaction reference
- Create a batch notarization system for multiple documents
- Implement verification that shows both blockchain timestamp and block time
- Build a simple audit trail system using sequential notarization
- Test verification failure with modified documents

## Troubleshooting

- **Hash verification failures**: ensure document content is identical, including encoding and line endings
- **Timestamp discrepancies**: distinguish between transaction creation time and block confirmation time
- **Privacy concerns**: remember that metadata stored on blockchain is publicly visible

## What this module covers

- Hash-based proof-of-existence and timestamping techniques
- Document notarization workflows and verification processes
- Privacy-preserving audit trail creation using blockchain immutability

## What this module does not cover

- Legal advice on notarization requirements in specific jurisdictions
- Advanced cryptographic techniques like zero-knowledge proofs
- Integration with traditional legal and notarial systems

## References and further reading

- Cryptographic hashing standards and best practices
- Blockchain timestamping legal precedents and recognition
- Audit trail and compliance documentation standards
