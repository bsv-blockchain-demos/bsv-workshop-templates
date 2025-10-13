---
title: "Tokenization with BSV-21 NFTs"
description: "Learn how to create, transfer, and manage NFTs using the BSV-21 token standard"
status: "Draft"
last_updated: ""
primitive_category: "Tokenization"
audience: "Intermediate"
---

# Tokenization with BSV-21 NFTs primitive module

## Learning objectives

- Understand the BSV-21 NFT standard and its data structure.
- Create (mint) NFTs with custom metadata through a simple UI.
- Transfer NFTs between wallets and see the transaction details.
- Programmatically verify NFT existence and ownership.
- Learn how to build NFT-based logic for access control.

## Summary

Learn how to create, transfer, and manage NFTs using the BSV-21 token standard. Participants will first interact with NFTs visually and then explore how NFT data is stored and validated on-chain.

## Core concept

NFTs (non-fungible tokens) represent unique digital assets with distinct properties. The BSV-21 standard defines how to create, transfer, and manage these tokens on the BSV blockchain using specific transaction formats.

## How it works on the BSV blockchain

- **Transaction structure**: NFT transactions include metadata in specific output formats following BSV-21 specifications
- **Script requirements**: uses standard transaction outputs with additional data fields for token information
- **Data format**: metadata stored as JSON or structured data within transaction outputs
- **Validation**: ownership verified through UTXO tracking and transaction history

## Practical implementation

The NFT workflow involves minting tokens with metadata, transferring ownership through standard transactions, and verifying current ownership by checking the blockchain state.

### Basic workflow

1. Create NFT with metadata (title, description, image)
2. Mint NFT by broadcasting creation transaction
3. Transfer NFT to another address
4. Verify ownership by reading blockchain state

### Code example

```js
// Minimal example showing NFT minting
async function mintNFT(metadata, ownerAddress, privateKey) {
  // Step 1: Create NFT data structure
  const nftData = {
    title: metadata.title,
    description: metadata.description,
    image: metadata.image,
  };
  // Step 2: Build mint transaction
  const mintTx = buildNFTMintTransaction(nftData, ownerAddress);
  // Step 3: Sign and broadcast
  const signed = signTransaction(mintTx, privateKey);
  return broadcastTransaction(signed);
}
```

## Common use cases

- Digital collectibles and artwork
- Access tokens for services or subscriptions
- Proof of ownership for physical or digital assets

## Current state and maturity

- **Implementation status**: BSV-21 standard is established and supported
- **Available tools**: SDKs available for NFT creation and management
- **Known limitations**: metadata size affects transaction costs

## Demo outline

Interactive web application demonstrating complete NFT lifecycle from creation to transfer.

### Demo objectives

- Participants will mint their first NFT with custom metadata
- They will transfer NFTs between wallets
- They will verify ownership programmatically

### Demo steps

1. Setup: connect to wallet or use provided credentials
2. Mint: create NFT with title, description, and image
3. List: view owned NFTs in a grid display
4. Transfer: send NFT to another address
5. Verify: check ownership status on blockchain

## Practical exercises

- Mint your first NFT with minimal metadata
- List all NFTs in a given wallet and display them in a grid
- Transfer an NFT to a partner's wallet and confirm it appears there
- Write a function verifyOwnership(tokenId, address) that returns true/false
- Burn an NFT and check that it is no longer spendable

## Troubleshooting

- **Mint transaction fails**: check metadata format and transaction fees
- **Transfer not appearing**: verify correct recipient address and confirmation status
- **Ownership verification issues**: ensure correct token ID and current blockchain state

## What this module covers

- BSV-21 NFT standard implementation and usage
- NFT creation, transfer, and ownership verification
- Basic metadata handling and display

## What this module does not cover

- Advanced smart contract functionality
- Complex royalty or marketplace mechanisms
- Large file storage solutions

## References and further reading

- BSV-21 token standard specification
- NFT metadata best practices
- Blockchain explorers supporting BSV-21 tokens
