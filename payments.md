---
title: "Payments on BSV blockchain workshop"
description: "Learn how to send and receive payments on the BSV blockchain through hands-on experience"
status: "Draft"
last_updated: "Friday, September 12, 2025"
audience: "Beginner to Intermediate"
level: "Intro"
duration: "3-4 hours"
prerequisites:
  [
    "Basic understanding of digital payments",
    "Familiarity with web browsers",
    "No prior blockchain experience required",
  ]
assets:
  ["Web wallet interface", "Block explorer access", "Test BSV for exercises"]
---

# Payments on BSV blockchain workshop

## Objectives

- Understand the UTXO model and how balance is calculated.
- Send and receive BSV payments using a simple web application.
- Build and sign a basic transaction programmatically.
- Get familiar with fees, confirmations, and potential pitfalls.

## Agenda

- Introduction to the BSV blockchain.
- Technology and ecosystem overview.
- Horizons and roadmap.
- Payments primitive module (core content).
- Demos and proofs of concept.
- Use cases for BSV payments.
- Code showcase and application.
- Practical exercises.
- Q&A and next steps.

## Introduction to blockchain

The BSV blockchain is a public ledger that records transactions between participants without requiring a central authority. Unlike traditional payment systems that maintain account balances, BSV uses an unspent transaction output (UTXO) model where each transaction consumes previous outputs and creates new ones.

Key concepts for this workshop:

- **Blocks**: collections of validated transactions grouped together
- **Transactions**: data structures that move value between addresses
- **UTXOs**: unspent outputs that represent spendable funds
- **Addresses**: public identifiers used to receive payments

The BSV blockchain's approach enables direct peer-to-peer payments with cryptographic security and immutable record-keeping.

## Technology deep dive

BSV payments work through a stateless transaction model where each payment can be validated independently. Key technical components include:

- **Transaction structure**: inputs consume previous outputs, outputs define new spending conditions
- **Digital signatures**: cryptographic proofs that transactions are authorised by private key holders
- **Script validation**: simple programs that define and verify spending conditions
- **Fee calculation**: payments to miners for transaction processing and inclusion in blocks

Supporting infrastructure includes:

- **Wallets**: applications that manage private keys and construct transactions
- **Broadcasting services**: networks that distribute transactions to miners
- **Block explorers**: web interfaces for viewing transaction and blockchain data

This technical foundation enables secure, peer-to-peer value transfer without intermediaries.

## Ecosystem overview

The BSV blockchain ecosystem includes various participants who facilitate payment functionality:

- **Miners**: validate transactions and produce blocks according to network rules
- **Wallet providers**: offer key management and transaction building services for users
- **Payment processors**: handle BSV payments for merchants and applications
- **Block explorers**: provide web interfaces for viewing transaction and address data
- **Exchange platforms**: facilitate trading between BSV and other currencies

Supporting services include:

- **APIs and SDKs**: developer tools for building BSV payment applications
- **Testing networks**: environments for development without using real BSV
- **Educational resources**: documentation and tutorials for developers and users

This ecosystem provides the infrastructure necessary for BSV payment adoption and integration.

## Horizons and roadmap

Current BSV payment capabilities include reliable transaction processing, low fees for micropayments, and extensive developer tooling. Areas of active development include:

- **Scaling improvements**: optimisations for increased transaction throughput
- **Developer tools**: enhanced SDKs and APIs for easier application development
- **Integration patterns**: standardised approaches for business and enterprise adoption
- **User experience**: improved wallet interfaces and payment workflows

The BSV blockchain's stability and large block capacity provide a foundation for continued growth in payment applications and integration opportunities.

## Payments primitive module

Learn how to send and receive payments on the BSV blockchain through a simple, interactive application. Participants will first experience payments from a user perspective and then explore how it works under the hood.

### Learning objectives

- Understand the UTXO model and how balance is calculated.
- Send and receive BSV payments using a simple web application.
- Build and sign a basic transaction programmatically.
- Get familiar with fees, confirmations, and potential pitfalls.

### Core concept

BSV payments work through the unspent transaction output (UTXO) model. Instead of account balances, the system tracks individual transaction outputs that can be spent as inputs to new transactions.

### How it works on the BSV blockchain

- **Transaction structure**: transactions consume previous outputs (inputs) and create new outputs, transferring value between addresses
- **Script requirements**: basic payment transactions use standard pay-to-public-key-hash (P2PKH) scripts
- **Data format**: transactions include inputs, outputs, fees, and digital signatures proving ownership
- **Validation**: the network validates transactions by checking signatures, input availability, and fee adequacy

### Practical implementation

The basic payment workflow involves listing available UTXOs, building a transaction, signing it with private keys, and broadcasting to the network.

#### Basic workflow

1. List UTXOs to calculate available balance
2. Build transaction with inputs, outputs, and appropriate fees
3. Sign transaction with private keys
4. Broadcast transaction to the network and monitor for confirmation

#### Code example

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

### Common use cases

- Peer-to-peer payments without intermediaries
- Micropayments for digital content or services
- Automated payments through programmatic interfaces

### Current state and maturity

- **Implementation status**: Production-ready with established standards
- **Available tools**: Multiple SDKs available in JavaScript, Python, and other languages
- **Known limitations**: Transaction fees vary with network conditions

## Demos and proofs of concept

This workshop includes hands-on demonstrations using a minimal web wallet application that allows participants to:

- **Send BSV**: enter address and amount, sign and broadcast transactions
- **Receive BSV**: show current address and QR code for receiving payments
- **View balance**: display current balance calculated by listing UTXOs
- **Check transaction history**: view past transactions and confirmation status

### Demo environment setup

- Web-based wallet interface (no software installation required)
- Test BSV provided for workshop exercises
- Block explorer access for transaction verification
- Backup transaction broadcasting service

### Progressive modules

1. **Visualise balance**: list UTXOs and calculate total balance
2. **Send and receive**: build, sign, and broadcast a basic transaction
3. **Transaction details**: inspect transaction structure, inputs/outputs, fees
4. **Confirmations**: check mempool status and first confirmation
5. **Automation (optional)**: simple watcher script for incoming transactions

## Use cases

BSV payments enable various practical applications where traditional payment systems face limitations:

### Digital payments

- **Direct peer-to-peer transfers**: send value without intermediaries or account approval
- **Cross-border payments**: transfer value globally without currency conversion fees
- **Micropayments**: enable small-value transactions not viable with traditional systems

### Business applications

- **Point-of-sale systems**: accept payments with immediate settlement
- **Subscription services**: automated recurring payments through smart contracts
- **Supply chain payments**: automatic payments triggered by delivery confirmation

### Developer integration

- **API monetisation**: charge per API call with micropayments
- **Content access**: pay-per-article or pay-per-view models
- **Gaming applications**: in-game purchases and player-to-player transfers

These use cases leverage BSV's low fees, fast confirmation times, and programmable functionality.

## Code showcase and application

### Application overview

The companion web application demonstrates core BSV payment functionality through a simple, interactive interface. Key features include:

- **Wallet functionality**: generate addresses, manage keys, calculate balances
- **Transaction building**: create, sign, and broadcast payment transactions
- **Blockchain integration**: read transaction data and confirm payments
- **User interface**: web-based interface requiring no software installation

### Key files and structure

- **index.html**: main application interface with payment forms
- **wallet.js**: wallet operations including key generation and balance calculation
- **transactions.js**: transaction building, signing, and broadcasting functions
- **utils.js**: utility functions for address validation and fee calculation

### Installation and setup

#### Prerequisites

- Modern web browser with JavaScript enabled
- Internet connection for blockchain API access
- Test BSV provided during workshop

#### Running the application

1. Open `index.html` in web browser
2. Generate or import wallet keys using the interface
3. View current balance calculated from UTXOs
4. Send payments to other workshop participants
5. Verify transactions using integrated block explorer

### Code walkthrough

Key implementation functions:

```js
// Balance calculation using UTXO aggregation
async function getBalance(address) {
    const utxos = await fetchUTXOs(address);
    return utxos.reduce((total, utxo) => total + utxo.value, 0);
    }
// Transaction building with proper input selection
function buildTransaction(utxos, toAddress, amount) {
    const selectedInputs = selectUTXOs(utxos, amount);
    const transaction = {
        inputs: selectedInputs.map(utxo => ({
            txid: utxo.txid,
            vout: utxo.vout,
            value: utxo.value
            })),
            outputs:
            { address: toAddress, value: amount },
            { address: changeAddress, value: calculateChange(selectedInputs, amount) }
            };
            return transaction;
            }
```

## Exercises

### Practical exercises
- Implement `getBalance()` function using UTXO aggregation
- Create and broadcast a simple payment transaction
- Verify transaction appears in a block explorer
- Build a script to monitor for incoming transactions

### Exercise structure
Each exercise includes:
- **Objective**: clear statement of what the exercise demonstrates
- **Task description**: step-by-step instructions for completion
- **Success criteria**: observable outcomes that indicate completion
- **Verification**: method to confirm the exercise worked correctly

### Progressive complexity
1. **Basic implementation**: use provided functions to send a payment
2. **Transaction analysis**: examine transaction structure and verify components
3. **Balance management**: implement UTXO tracking and balance calculation
4. **Error handling**: deal with insufficient funds and invalid addresses
5. **Automation**: create simple scripts for payment monitoring

## Troubleshooting

### Common issues
- **Insufficient funds**: verify balance accounts for transaction fees
- **Transaction not confirming**: check fee amount and mempool status
- **Invalid signature**: ensure correct private key and transaction format
- **Network connectivity**: confirm API access and service availability

### Diagnostic approach
- Document exact error messages and steps taken
- Check prerequisites and configuration settings
- Test with minimal examples to isolate issues
- Review transaction structure and validation requirements

### Resolution strategies
- **Fee calculation**: use current network fee rates for reliable confirmation
- **Key management**: verify private key format and derivation
- **Network issues**: try alternative API endpoints or wait for service restoration
- **Transaction building**: validate input UTXOs and output addresses

## Assessment and feedback

### Learning verification
- **Practical completion**: confirm participants successfully sent and received payments
- **Understanding checks**: verify comprehension through questions about UTXO model
- **Application demonstration**: participants explain transaction flow

### Knowledge checks
- Can you explain how balance is calculated using UTXOs?
- What are the main steps to send a BSV payment?
- How do transaction fees affect payment confirmation?
- Where would you look for help with payment integration?

### Completion criteria
Participants successfully complete the workshop when they:
- Send a payment to another participant with confirmation
- Demonstrate understanding of UTXO model through balance calculation
- Successfully troubleshoot a common payment issue

## Appendix

### Glossary
**BSV blockchain**: the public blockchain network using the original Bitcoin protocol rules.

**BSV**: the native token used for transactions on the BSV blockchain.

**UTXO**: unspent transaction output, representing spendable value in the system.

**Transaction**: a data structure that transfers value between addresses by consuming inputs and creating outputs.

**Address**: a public identifier derived from a public key, used to receive payments.

**Private key**: a secret number used to sign transactions and prove ownership of funds.

**Fee**: payment to miners for including transactions in blocks.

**Confirmation**: the process of including a transaction in a block and subsequent blocks.

### Technical references
- BSV protocol specifications and transaction format documentation
- JavaScript SDK documentation and API references
- Block explorer services for transaction verification
- Testing network information and faucet services

### Version information
- Workshop version: 1.0.0
- Compatible BSV SDK versions: 1.0.x and above
- Last updated: Friday, September 12, 2025
