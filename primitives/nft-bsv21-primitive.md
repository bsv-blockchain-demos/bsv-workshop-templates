---
title: "NFT management with BSV-21"
description: "Create, transfer, and verify non-fungible tokens using the BSV-21 standard"
status: "Draft"
last_updated: ""
primitive_category: "NFT"
audience: "Intermediate"
---

# NFT management with BSV-21 primitive module

## Learning objectives

- Understand the BSV-21 NFT standard and its data structure.
- Create (mint) NFTs with custom metadata through a simple UI.
- Transfer NFTs between wallets and see the transaction details.
- Programmatically verify NFT existence and ownership.
- Learn how to build NFT-based logic for access control or subscriptions.

## Summary

Learn how to create, transfer, and manage NFTs using the BSV-21 token standard. Participants will first interact with NFTs visually and then explore how NFT data is stored and validated on-chain.

## Core concept

NFTs are non-fungible tokens that represent unique digital assets. The BSV-21 standard defines how to create, transfer, and manage these tokens on the BSV blockchain using specific transaction formats and metadata structures.

## How it works on the BSV blockchain

- **Transaction structure**: NFT transactions include structured metadata following BSV-21 specifications
- **Script requirements**: uses standard transaction outputs with additional data fields for token information
- **Data format**: metadata stored as structured data within transaction outputs, typically JSON format
- **Validation**: ownership tracked through UTXO model, verified by transaction history

## Practical implementation

The NFT workflow involves minting tokens with metadata, managing transfers through standard transactions, and verifying ownership by reading blockchain state.

### Basic workflow

1. Mint NFT with title, description, and image metadata
2. List owned NFTs by reading blockchain state
3. Transfer NFT to another wallet address
4. Verify ownership programmatically

### Code example

```js
// Minimal example showing NFT operations
async function mintNFT(metadata, ownerAddress, privateKey) {
  const nftData = {
    title: metadata.title,
    description: metadata.description,
    image: metadata.image,
  };
  const mintTx = buildBSV21MintTransaction(nftData, ownerAddress);
  const signed = signTransaction(mintTx, privateKey);
  return broadcastTransaction(signed);
}
async function verifyOwnership(tokenId, address) {
  const utxos = await getUTXOsForAddress(address);
  return utxos.some((utxo) => utxo.tokenId === tokenId);
}
```

## Common use cases

- Digital collectibles and artwork
- Access tokens for services or subscriptions
- Proof of membership or certification
- Unique identifiers for physical assets

## Current state and maturity

- **Implementation status**: BSV-21 standard is established and widely supported
- **Available tools**: Multiple SDKs support BSV-21 NFT operations
- **Known limitations**: metadata size affects transaction costs; large images require external storage

## Demo outline

Interactive web application demonstrating complete NFT lifecycle from creation to ownership verification.

### Demo objectives

- Participants will mint NFTs with custom metadata
- They will view and manage their NFT collection
- They will transfer NFTs and verify ownership changes

### Demo steps

1. Setup: connect to wallet or use provided test credentials
2. Mint: create NFT with title, description, and image
3. List: view owned NFTs in a grid display with metadata
4. Transfer: send NFT to another address
5. Verify: check ownership programmatically
6. Optional: burn NFT and confirm it no longer exists

## Practical exercises

- Mint your first NFT with minimal metadata
- List all NFTs in a given wallet and display them in a grid
- Transfer an NFT to a partner's wallet and confirm it appears there
- Write a function `verifyOwnership(tokenId, address)` that returns true/false
- Optional: burn an NFT and check that it is no longer spendable

## Troubleshooting

- **Mint transaction fails**: verify metadata format and sufficient fees for transaction size
- **NFT not appearing in list**: check transaction confirmation and indexing delays
- **Transfer not completing**: ensure correct recipient address format and network connectivity

## What this module covers

- BSV-21 NFT standard implementation and best practices
- NFT creation, transfer, and ownership verification workflows
- Integration patterns for access control and verification logic

## What this module does not cover

- Complex smart contract functionality beyond basic NFT operations
- Advanced marketplace or royalty distribution mechanisms
- Large file storage solutions or IPFS integration

## References and further reading

- BSV-21 token standard specification
- BSV blockchain documentation for transaction formats
- NFT metadata standards and best practices
