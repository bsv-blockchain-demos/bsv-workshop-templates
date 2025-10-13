---
title: "Data inscription on BSV blockchain"
description: "Store, encrypt, and retrieve arbitrary data directly on the BSV blockchain"
status: "Draft"
last_updated: ""
primitive_category: "Data Storage"
audience: "Intermediate"
---

# Data inscription on BSV blockchain primitive module

## Learning objectives
- Understand how data is stored in transactions (OP_RETURN, pushdata).
- Learn to hash data and store only its hash for proof-of-existence.
- Save arbitrary data (JSON, text, small files) directly on-chain.
- Retrieve and decode data from the blockchain.
- Encrypt and decrypt data before storing for privacy.
- Explore practical benefits (auditing, timestamping, trustless verification).

## Summary
Learn how to store, encrypt, and retrieve arbitrary data directly on the BSV blockchain. Participants will see how to inscribe data, hash content, and verify it later, as well as understand the benefits of on-chain storage and privacy techniques.

## Core concept
Data inscription allows arbitrary information to be stored permanently on the blockchain using transaction outputs. This provides immutable storage with cryptographic proof of existence and timestamp verification.

## How it works on the BSV blockchain
- **Transaction structure**: data stored in OP_RETURN outputs or as push data in transaction scripts
- **Script requirements**: uses OP_RETURN opcode or standard data push operations
- **Data format**: arbitrary bytes, commonly JSON, text, or binary data
- **Validation**: data integrity verified through transaction hash and Merkle proofs

## Practical implementation
The data inscription workflow involves preparing data, optionally encrypting it, storing it in a transaction, and later retrieving and verifying the stored information.

### Basic workflow
1. Prepare data (text, JSON, or small files)
2. Optionally hash data for proof-of-existence
3. Optionally encrypt data with passphrase
4. Store data in OP_RETURN transaction output
5. Retrieve data by transaction ID and verify integrity

### Code example
```js
// Minimal example showing data inscription
async function inscribeData(data, encrypt = false, passphrase = null) {
    let processedData = data;
    // Step 1: Optionally encrypt data
    if (encrypt && passphrase) {
        processedData = encryptData(data, passphrase);
        }
    // Step 2: Create hash for verification
    const dataHash = sha256(processedData);
    // Step 3: Build transaction with OP_RETURN
    const tx = buildDataTransaction(processedData);
    // Step 4: Broadcast transaction
    return broadcastTransaction(tx);
    }
async function retrieveData(txid, decrypt = false, passphrase = null) {
    const data = await getDataFromTransaction(txid);
    return decrypt ? decryptData(data, passphrase) : data
    }
```

## Common use cases
- Document timestamping and proof-of-existence
- Audit trails and immutable logs
- Small file storage with cryptographic verification
- Encrypted private data storage

## Current state and maturity
- **Implementation status**: Well-established pattern with proven implementations
- **Available tools**: Multiple SDKs support OP_RETURN data inscription
- **Known limitations**: Data size affects transaction fees; large files require chunking

## Demo outline
Interactive web application demonstrating complete data inscription workflow from storage to retrieval and verification.

### Demo objectives
- Participants will store various types of data on-chain
- They will retrieve and verify data integrity
- They will understand encryption/decryption workflows

### Demo steps
1. Setup: connect to wallet or use provided credentials
2. Hash: compute SHA-256 hash of input data
3. Store: inscribe data using OP_RETURN in transaction
4. Retrieve: fetch data by transaction ID
5. Verify: compare retrieved data hash with original
6. Optional: encrypt data before storage and decrypt after retrieval

## Practical exercises
- Hash a local file and display its SHA-256 digest
- Store a simple message on-chain using OP_RETURN
- Retrieve the message using transaction ID and display it
- Encrypt a message with a password, store and then decrypt it
- Implement `verifyDataIntegrity(originalData, txid)` to confirm on-chain match

## Troubleshooting
- **Data too large**: consider storing hash only or splitting into multiple transactions
- **Encryption errors**: verify passphrase consistency between encrypt and decrypt operations
- **Retrieval failures**: check transaction confirmation and data format expectations

## What this module covers
- OP_RETURN data inscription patterns and best practices
- Data hashing, encryption, and integrity verification
- Practical applications for immutable data storage

## What this module does not cover
- Large file storage solutions or distributed storage integration
- Complex data structures or database-like query capabilities
- Advanced cryptographic schemes beyond basic encryption

## References and further reading
- BSV protocol documentation for OP_RETURN usage
- Cryptographic hashing and encryption best practices
- Blockchain explorers supporting data transaction viewing

