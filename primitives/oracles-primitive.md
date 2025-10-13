---
title: "Oracles and external data"
description: "Bringing external data onto the BSV blockchain for smart contract integration"
status: "Draft"
last_updated: ""
primitive_category: "Oracles"
audience: "Advanced"
---

# Oracles and external data primitive module

## Learning objectives

- Understand how oracles bridge external data sources with blockchain applications.
- Learn to implement basic oracle patterns for price feeds and external verification.
- Build applications that consume oracle data for automated decision-making.
- Design secure oracle systems that resist manipulation and ensure data integrity.

## Summary

Learn how to integrate external data sources with BSV blockchain applications using oracle patterns. Participants will explore how to bring real-world data onto the blockchain and use it in smart contracts and automated systems.

## Core concept

Oracles are services that provide external data to blockchain applications, enabling smart contracts to react to real-world events like price changes, weather data, or external system states that cannot be directly accessed from within the blockchain.

## How it works on the BSV blockchain

- **Transaction structure**: oracle data stored in OP_RETURN outputs with signed attestations
- **Script requirements**: contracts can verify oracle signatures and data validity
- **Data format**: structured data with cryptographic signatures proving authenticity
- **Validation**: oracle data verified through digital signatures and reputation systems

## Practical implementation

The oracle workflow involves data collection from external sources, signing data with oracle private keys, publishing signed data to the blockchain, and consuming oracle data in applications.

### Basic workflow

1. Collect data from external sources (APIs, sensors, etc.)
2. Sign data with oracle private key to attest authenticity
3. Publish signed data to blockchain in structured format
4. Applications consume oracle data and verify signatures

### Code example

```js
// Minimal example showing oracle implementation
class Oracle {
  constructor(privateKey, publicKey) {
    this.privateKey = privateKey;
    this.publicKey = publicKey;
  }
  async publishData(dataSource, value, timestamp) {
    // Step 1: Create data payload
    const payload = {
      source: dataSource,
      value: value,
      timestamp: timestamp,
      oracle: this.publicKey,
    };
    // Step 2: Sign data with oracle private key
    const signature = signData(JSON.stringify(payload), this.privateKey);

    // Step 3: Publish to blockchain
    const oracleData = { ...payload, signature };
    const tx = buildOracleTransaction(oracleData);

    return broadcastTransaction(tx);
  }
}
async function consumeOracleData(txid, oraclePublicKey) {
  const oracleData = await getOracleDataFromTransaction(txid);
  // Verify oracle signature
  const isValid = verifySignature(
    JSON.stringify(oracleData.payload),
    oracleData.signature,
    oraclePublicKey
  );
  return { oracleData, verified: isValid };
}
```

## Common use cases

- Price feeds for financial applications and DeFi protocols
- Weather data for insurance and agricultural applications
- Sports results and event outcomes for betting applications
- IoT sensor data for supply chain and monitoring systems

## Current state and maturity

- **Implementation status**: Basic oracle patterns are established; advanced systems under development
- **Available tools**: Oracle libraries and data feed services available
- **Known limitations**: Oracle reliability depends on data source quality and operator reputation

## Demo outline

Interactive web application demonstrating oracle data publication and consumption workflows.

### Demo objectives

- Participants will create and operate a simple oracle service
- They will publish external data to the blockchain with cryptographic attestation
- They will build applications that consume and verify oracle data

### Demo steps

1. Setup: configure oracle service with data sources and signing keys
2. Collect: gather data from external APIs or manual input
3. Publish: sign and broadcast oracle data to blockchain
4. Consume: read oracle data in client application and verify signatures
5. React: demonstrate automated responses to oracle data changes

## Practical exercises

- Create a simple price feed oracle that publishes current BSV price
- Build an application that reads oracle data and displays it with verification status
- Implement signature verification for oracle data authenticity
- Design a multi-oracle system that aggregates data from multiple sources
- Create automated triggers that respond to specific oracle data conditions

## Troubleshooting

- **Signature verification failures**: ensure consistent data serialisation between signing and verification
- **Data freshness issues**: implement timestamp validation and data expiry logic
- **Oracle reliability problems**: design redundancy and consensus mechanisms for critical applications

## What this module covers

- Basic oracle implementation patterns and data attestation
- Oracle data consumption and verification in applications
- Security considerations for oracle design and operation

## What this module does not cover

- Advanced oracle networks or decentralised oracle protocols
- Complex aggregation algorithms or consensus mechanisms
- Economic incentives and governance models for oracle networks

## References and further reading

- Oracle design patterns and security best practices
- Digital signature verification and cryptographic attestation
- External data integration patterns for blockchain applications
