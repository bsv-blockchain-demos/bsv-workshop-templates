---
title: Data inscription on BSV blockchain workshop
description: Learn to store, encrypt, and retrieve arbitrary data on the BSV blockchain using OP_RETURN and pushdata, with hands-on demos and code walkthroughs
status: Draft
lastupdated: Monday, September 22, 2025
audience: Beginner to Intermediate level
Intro duration: 3-4 hours
prerequisites:
  - Basic understanding of web apps and HTTP APIs
  - Familiarity with JavaScript is helpful
  - No prior blockchain experience required
assets:
  - Data inscription demo web app
  - Block explorer access
  - Test BSV for exercises
---

# Data inscription on BSV blockchain workshop

## Objectives

- Understand how data is inscribed in transactions using OP_RETURN or pushdata, and how this differs from account-based data storage.
- Hash data for proof-of-existence and verify integrity later using retrieved on-chain bytes.
- Save JSON, text, and small binary payloads to the blockchain and read them back programmatically.
- Apply optional encryption and decryption steps for privacy-preserving on-chain storage.
- Build and broadcast a minimal inscription transaction and verify it in a block explorer.

## Agenda

- Introduction to data inscription and what “on-chain data” means on BSV.
- Technology overview: OP_RETURN, pushdata, hashing, encryption, and retrieval paths.
- Demo: inscribe, retrieve, verify, and optionally encrypt data end to end.
- Use cases: timestamping, audit trails, immutable logs, and small file proofs.
- Code showcase and application architecture overview. 
- Practical exercises: build, broadcast, retrieve, and verify.
- Troubleshooting, assessment, and feedback.

## Introduction

The BSV blockchain allows arbitrary data to be stored inside transaction outputs using OP_RETURN and standard pushdata operations, enabling immutable data anchoring directly on the ledger.
Unlike account-based ledgers, BSV’s UTXO model encodes state through spendable outputs, and data inscriptions live as payloads in scripts verified and timestamped by miners.
This workshop focuses on preparing data, hashing and encrypting it when appropriate, inscribing it on-chain, and retrieving it later for verification or display.

## Technology deep dive

- Transaction structure: data may be stored in an OP_RETURN output or pushed as script data, with zero spendability by design for OP_RETURN.
- Script requirements: OP_RETURN terminates script verification and carries data pushes, while standard data pushes can be included in non-spendable patterns.
- Data format: arbitrary bytes are supported, commonly JSON for structured data or binary for compact artifacts.
- Validation: data integrity is verified by recomputing hashes and by checking the transaction’s inclusion and Merkle path.

### Concepts

- SDKs, explorer APIs, and wallet integrations can construct and broadcast transactions with OP_RETURN outputs.
- Explorers reveal OP_RETURN fields, and wallets manage keys and UTXO selection for fees and confirmations.
- Tooling supports the flow from data preparation to broadcast and later retrieval by txid.

## Ecosystem overview

- Tooling for chunked inscriptions, metadata conventions, and encryption workflows is evolving.
- Best practice: hash large files and store only digests or references; store full payloads for smaller data.
- SDK and indexing improvements enable simpler retrieval and verification experiences.

## Horizons and roadmap

- Understand OP_RETURN and pushdata-based storage and where each is appropriate.
- Hash input data for proof-of-existence and later integrity checks.
- Encrypt and decrypt data to protect sensitive content.
- Build, sign, broadcast, and verify a minimal inscription transaction end to end.

## Primitive module

### Learning objectives

- Store, encrypt, and retrieve arbitrary data directly on-chain.
- Inscribe data, hash content, and verify later with privacy options.

### Core concept

- Transaction structure: inputs consume UTXOs and outputs include one OP_RETURN with data payload.
- Script requirements: OP_RETURN + pushdata encodes bytes; other outputs provide change and fees.
- Data format: JSON, UTF-8 text, or binary blobs within size and fee limits.
- Validation: recompute hashes and confirm transaction inclusion.

### Practical implementation

1. Prepare text, JSON, or small files.
2. Optionally encrypt data before inscription.
3. Compute SHA-256 hash of original or encrypted payload.
4. Build a transaction with OP_RETURN carrying the bytes and estimate fees.
5. Broadcast and record the txid for retrieval and verification.

#### Basic workflow (pseudo-code)

```js
// Minimal example showing data inscription
async function inscribeData(data, encrypt = false, passphrase = null) {
  let processedData = data; // 1) optionally encrypt
  if (encrypt && passphrase) processedData = encryptData(data, passphrase);
  const dataHash = sha256(processedData); // 2) hash for verification
  const tx = buildDataTransaction(processedData); // 3) build OP_RETURN
  const txid = await broadcastTransaction(tx); // 4) broadcast
  return { txid, dataHash };
}
async function retrieveData(txid, decrypt = false, passphrase = null) {
  const data = await getDataFromTransaction(txid);
  return decrypt && passphrase ? decryptData(data, passphrase) : data;
}
```



## Common use cases

- Document timestamping and proof-of-existence when only the digest is needed on-chain.
- Audit trails and immutable event logs that require dependable ordering and integrity.
- Small file storage with cryptographic verification or pointers for larger assets.
- Encrypted records where content must be recoverable but not publicly readable.

## Current state and maturity

- Implementation status: OP_RETURN inscription is widely used and supported.
- Available tools: multiple SDKs and explorers read/write OP_RETURN data.
- Known limitations: larger payloads cost more and may require chunking or off-chain storage with on-chain hashes.

## Demos and proofs of concept

- Hands-on demo: encryption, hashing, inscription, retrieval, and verification end to end.
- Explorer integration: view OP_RETURN and confirm inclusion by txid.
- Optional advanced mode: chunked payloads or encrypted fields.

### Demo environment setup

- Web app, test BSV, explorer access, and sample data.
- Wallet connectivity or test credentials to build and broadcast transactions.

### Progressive modules

1. Setup: connect wallet or use provided credentials.
2. Hash: compute SHA-256 of sample text or JSON.
3. Store: inscribe data with OP_RETURN and capture txid.
4. Retrieve: fetch OP_RETURN by txid and decode.
5. Verify: compare hashes to confirm integrity and timestamp.
6. Optional: encrypt before storage and decrypt after retrieval.

## Use cases

- Digital content proofs: publish hashes for verifiable provenance.
- Compliance and audit trails: append-only logs with verifiable entries.
- Proof-of-existence: notarize agreements or research data via digests.
- Encrypted records: sensitive notes or keys with controlled decryption.

## Code showcase and application

### Application overview

- End-to-end inscription workflow with clear separation of hashing, encryption, tx building, and retrieval.
- Explorer links for confirmation and SDK functions for UTXO management and OP_RETURN creation.

### Key files and structure

- app.html: UI for data entry, options, and results.
- inscription.js: hashing, optional encryption, tx construction, broadcast.
- wallet.js: UTXO listing, fee calculation, signing.
- utils.js: encoding, hex conversion, explorer helpers.

### Installation and setup

- Prerequisites: browser, network access to blockchain APIs, test BSV, sample JSON/text.
- Running: connect wallet, inscribe sample data, verify in explorer, retrieve and validate hash.

#### Key implementation functions (pseudo-code)
```js
// Hashing utility for proof-of-existence
async function computeDigest(bytes) {
    return sha256(bytes);
    }
// Build OP_RETURN inscription output
function buildInscriptionOutput(dataHex) {
    return Script.fromASM(`OP_RETURN ${dataHex}`);
    }
// Assemble and broadcast an inscription transaction
async function inscribe(bytes) {
    const hex = Buffer.from(bytes).toString(‘hex’);
    const opret = buildInscriptionOutput(hex);
    const tx = await buildTransactionWithOutput(opret);
    return broadcastTransaction(tx);
    }
```



## Exercises

- Minimal inscription: inscribe a short message and verify on explorer.
- Integrity proof: inscribe a file digest and confirm later.
- Encrypted note: encrypt, store, retrieve, and decrypt a secret.
- Data policy: decide hash-only vs full payload and justify.
- Programmatic retrieval: write a retriever/verifier by txid.

### Troubleshooting

- Data too large: prefer digest-only or chunk across transactions.
- Encryption errors: verify passphrase consistency and encoding.
- Retrieval failures: ensure confirmation and correct OP_RETURN parsing.
- Fee issues: adjust payload size and check current fee rates.

### Diagnostic approach

- Capture exact errors and payload sizes used.
- Verify prerequisites, wallet connectivity, and endpoints.
- Reduce to minimal bytes to isolate encoding/size issues.
- Confirm explorer decoding and OP_RETURN script hex correctness.

### Resolution strategies

- Prefer hash-only for large artifacts with off-chain storage.
- Use consistent encoding and strong passphrases.
- Validate fee estimation for payload size and network.
- Retry with alternative API endpoints on transient failures.

## Assessment and feedback

### Learning verification

- Practical completion: inscribe, retrieve, and verify data.
- Understanding checks: explain OP_RETURN, hashing, encryption choices.
- Application demonstration: describe transaction structure and verification flow.

### Knowledge checks

- What is the role of OP_RETURN in data inscription on BSV?
- When should a project store a hash versus the full payload?
- How does encryption fit into an inscription workflow?
- What steps verify on-chain integrity after retrieval?

### Completion criteria

- Participant completed inscription and retrieval with verification.
- Can articulate trade-offs between payload size, fees, and privacy.
- Demonstrates programmatic retrieval and OP_RETURN decoding.

## Appendix

### Glossary

- OP_RETURN: attaches data to a transaction output without spendability.
- Push inserts arbitrary bytes into a script.
- Proof-of-existence: anchoring a hash of content on-chain for timestamped integrity verification.
- Encryption: encoding data such that only key holders can decrypt it.
- Digest: cryptographic hash used for integrity checks and identity of data.
- UTXO: unspent transaction output, BSV’s state model.

### Technical references

- BSV protocol documentation and OP_RETURN usage.
- Hashing and encryption best practices.
- Explorer APIs and tools for decoding OP_RETURN payloads.
- SDK docs for building and broadcasting transactions.

### Version information

- Workshop version: 1.0.0.
- Compatible BSV SDK versions: 1.0.x and above.
- Last updated: Monday, September 22, 2025.
