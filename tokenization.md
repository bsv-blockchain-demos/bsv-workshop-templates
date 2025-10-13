---
title: "Tokenization on BSV blockchain workshop"
description: "Learn to create, transfer, and manage tokens (fungible and non-fungible) on the BSV blockchain through hands-on experience"
status: "Draft"
last_updated: "Monday, September 15, 2025"
audience: "Beginner to Intermediate"
level: "Intro"
duration: "4 hours"
prerequisites:
  [
    "Basic understanding of digital payments",
    "Familiarity with web browsers",
    "Exposure to JavaScript or similar programming is useful",
  ]
assets:
  [
    "Tokenization demo web app",
    "Block explorer access",
    "Test BSV for minting fees",
  ]
---

# Tokenization on BSV blockchain workshop

## Objectives

- Understand the difference between fungible and non-fungible tokens (NFTs)
- Learn the fundamentals of the BSV token model and standards (e.g., BSV-21)
- Mint, transfer, and verify both fungible tokens and NFTs on the BSV blockchain
- Integrate token logic programmatically using provided SDKs and example apps

## Agenda

- Introduction to the concept of tokenization and asset digitisation
- BSV technology overview for tokens and NFTs
- Ecosystem and standards for tokenization (BSV-21, data schemas)
- Demo: Token minting, transfer, and verification
- Use cases for BSV tokenization
- Code showcase and walkthrough
- Practical exercises (build, mint, and transfer tokens/NFTs)
- Troubleshooting, assessment, and feedback

## Introduction to tokenization

Tokenization is the process of representing physical or digital assets as tokens on a blockchain. On BSV, tokenization enables the creation, transfer, and management of both fungible tokens (e.g., points, currencies) and non-fungible tokens (NFTs: unique digital assets such as collectibles or certificates).

Key concepts:

- **Tokens**: digital representations of assets with on-chain ownership
- **Fungible tokens**: interchangeable units (e.g., stablecoins, loyalty points)
- **Non-fungible tokens (NFTs)**: unique, individually identified assets
- **Minting**: creating new tokens and recording them on-chain
- **Transfer**: sending tokens between blockchain addresses

These features make BSV a powerful platform for building both consumer and business tokenised solutions.

## Technology deep dive

The BSV blockchain supports tokenization using on-chain scripting, data inscription, and open token standards such as BSV-21. Technical considerations:

- **Token standards**: define data structure, issuance, and transfer logic
- **Transaction structure**: tokens are minted with special outputs referencing metadata
- **NFT metadata**: JSON or structured data included in transaction outputs
- **Ownership model**: UTXO-based, so tokens/NFTs are transferred by spending outputs
- **Validation**: tokens are verified by tracking UTXO ownership and reading metadata

Supporting infrastructure includes:

- **Wallets**: supporting token and NFT management
- **Indexers/explorers**: display token ownership, attributes, and transaction history
- **SDKs**: enable minting and transfer in code (e.g., JavaScript, Python SDKs)

## Ecosystem overview

BSV tokenization is supported by a growing ecosystem:

- **Standard protocols**: BSV-21 (NFTs), fungible token conventions
- **Wallets**: web wallets and apps with token support
- **Marketplaces**: NFT and digital asset trading platforms
- **Developer tools**: SDKs and API services for token interaction
- **Block explorers**: show token metadata and provenance

Community-driven standards and public protocols enable interoperability and innovation across projects and platforms.

## Horizons and roadmap

Active development areas in BSV tokenization:

- Standardisation and improvements in on-chain NFT/token protocols
- Tooling to simplify mass minting, transfer, and asset management
- Bridges between BSV tokens and other blockchain/legacy systems
- Advanced NFT features (royalties, multi-asset support, fractionalisation)
- Expansion of real-world use cases (tickets, memberships, certifications, gaming)

Stability and scalability of the BSV blockchain provides a robust foundation for future growth in tokenized applications.

## Tokenization primitive module

### Learning objectives

- Understand the data structures for both fungible and non-fungible tokens on BSV
- Mint tokens/NFTs and record asset metadata on-chain
- Transfer tokens/NFTs between addresses
- Verify token authenticity and ownership programmatically

### Core concept

BSV tokenization leverages UTXO model to represent assets as spendable transaction outputs, using metadata to distinguish token type and properties.

### How it works on the BSV blockchain

- **Transaction structure**: token/NFT transactions include metadata or pointers in output scripts (e.g., OP_RETURN)
- **Script requirements**: most tokens use P2PKH for transferability; NFTs use additional data fields
- **Data format**: JSON-formatted metadata for NFTs (title, image, description), issuance/count for fungible tokens
- **Validation**: token/NFT ownership determined by script and UTXO tracking; authenticity by verifying issuer and metadata

### Practical implementation

Minting and transferring tokens follow these steps:

1. Prepare metadata or token definition (for NFT: title, description, image hash)
2. Create a mint transaction with metadata in output
3. Broadcast and confirm the mint transaction
4. Transfer token/NFT by building, signing, and broadcasting a transfer transaction

#### Code example

```js
// Mint an NFT on BSV using a JavaScript SDK (simplified)
async function mintNFT(metadata, ownerAddress, issuerPrivateKey) {
  // Step 1: Format metadata (e.g. as JSON string)
  const meta = JSON.stringify(metadata);
  // Step 2: Build mint transaction with metadata as OP_RETURN
  const mintTx = buildNFTMintTransaction(meta, ownerAddress);
  // Step 3: Sign and broadcast
  const signedTx = signTransaction(mintTx, issuerPrivateKey);
  return broadcastTransaction(signedTx);
}
// Transfer an NFT
async function transferNFT(nftUtxo, toAddress, ownerPrivateKey) {
  const transferTx = buildNFTTransferTransaction(nftUtxo, toAddress);
  const signedTx = signTransaction(transferTx, ownerPrivateKey);
  return broadcastTransaction(signedTx);
}
```

### Common use cases

- Digital collectibles and artwork (NFTs)
- Tickets and event passes
- Memberships and certifications
- Proof-of-ownership for physical assets
- In-game assets and digital currencies
- Voucher and coupon systems

### Current state and maturity

- **Implementation status**: Token/NFT protocols are deployed and used in production
- **Available tools**: JavaScript/Python SDKs, marketplaces, NFT minting services available
- **Known limitations**: Large token/NFT metadata increases transaction size/fees; compliance varies for asset classes

## Demos and proofs of concept

Hands-on demo with a minimal web app:

- **Mint NFT/token**: enter metadata, supply, and mint to your workshop wallet
- **View my tokens**: display wallets' NFTs and fungible balances
- **Transfer**: send tokens/NFTs to other workshop participants
- **Verify**: confirm NFT/token in block explorer; view metadata

### Demo environment setup

- Workshop supplies test BSV and access to web wallet
- Demo app pre-configured for testnet/mainnet, if needed
- NFT/media generator for quick workshop minting

## Use cases

- **Digital art and collectibles**: create and trade unique NFTs representing digital goods
- **Access control**: NFTs/tokens as membership cards for online communities
- **Proof-of-authenticity**: timestamp artist signatures or product origins
- **Rewards and loyalty**: loyalty points as fungible tokens for retention programs
- **Gaming**: in-game items and economies tokenised for direct transfer

## Code showcase and application

### Application overview

- **Web app**: mint, view, transfer, and verify tokens/NFTs
- **Key files**:
  - `app.html`: browser-based UI
  - `token.js`: minting, transferring, verification logic
  - `wallet.js`: address and UTXO management
  - `utils.js`: metadata, QR, and explorer integration

### Code walkthrough

```js
// Mint a fungible token on BSV (simplified)
async function mintToken(supply, name, symbol, ownerAddress, issuerPrivateKey) {
  const tokenData = { supply, name, symbol };
  const mintTx = buildTokenMintTransaction(tokenData, ownerAddress);
  const signedTx = signTransaction(mintTx, issuerPrivateKey);
  return broadcastTransaction(signedTx);
}
// Query all NFTs owned by a wallet
async function listMyNFTs(address) {
  const utxos = await fetchUTXOs(address);
  return utxos.filter((utxo) => utxo.isNFT);
}
```

## Exercises

- Mint your own NFT by entering creative metadata
- View and verify NFT/token ownership in the block explorer
- Transfer your NFT to another participant and confirm receipt
- Mint a fungible token (e.g., "Workshop Token") and distribute units among peers
- Write a script to verify a token's authenticity by checking issuer metadata

## Troubleshooting

- **Metadata too large**: truncate or store asset off-chain with on-chain pointer/hash
- **Transfer not appearing**: confirm transaction status and correct address
- **Wallet doesn't show token**: ensure correct indexers and token protocols supported
- **Fee too high**: check transaction size and batch minting where possible

## Assessment and feedback

### Learning verification

- Minted and transferred tokens/NFTs successfully
- Demonstrated ability to verify asset metadata and ownership on explorer
- Understood differences between fungible tokens and NFTs

### Knowledge checks

- What is an NFT, and how does BSV represent its metadata?
- How are fungible tokens transferred using UTXOs?
- What are some business applications of tokenization?
- How can token authenticity be verified programmatically?

### Completion criteria

- Participant minted, viewed, and transferred an NFT/token
- Can explain the on-chain representation of tokens on BSV
- Confident with basic BSV token/NFT programmatic operations

## Appendix

### Glossary

**Token**: Digital asset represented as a spendable output on blockchain
**NFT**: Non-fungible token, a unique asset identified by on-chain metadata
**Minting**: Creating new tokens/NFTs and assigning initial ownership
**Metadata**: Structured data defining an NFT's unique properties
**UTXO**: Unspent transaction output, BSV blockchain's base asset representation
**Burning**: Permanently removing a token/NFT by spending output to an unspendable address

### Technical references

- BSV-21 and related NFT/token protocol documentation
- SDK references (JavaScript, Go, Python)
- NFT/token metadata conventions and best practices
- Explorer APIs for NFT/token verification

### Version information

- Workshop version: 1.0.0
- Compatible BSV SDK versions: 1.0.x and above
- Last updated: Monday, September 15, 2025

