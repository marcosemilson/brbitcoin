# BTC SDK - TypeScript Edition

A lightweight and extensible SDK for Bitcoin transaction handling and wallet management. This SDK provides developers with tools to interact with the Bitcoin blockchain, manage wallets, create transactions, and work with custom scripts like P2SH and multisig addresses.

## Features

- **Wallet Management**:
  - Generate Hierarchical Deterministic (HD) wallets (BIP39/BIP44 compliant).
  - Support for SegWit (Bech32) and legacy addresses.
- **Transaction Creation**:
  - Create and sign Bitcoin transactions.
  - Support for custom scripts (P2SH, multisig).
- **Blockchain Interaction**:
  - Fetch address information (balance, UTXOs).
  - Query transactions and blocks.
- **Integration with Bitcoin Nodes**:
  - Support for Bitcoin Core JSON-RPC integration.
- **Security**:
  - Private key backup and restoration.
  - Fully typed and secure.

## Installation

Install the required dependencies:

```bash
npm install bitcoinjs-lib bip39 bip32 axios
```

## Usage

### Generate a Wallet

```typescript
import { generateWallet } from './btc-sdk';

const wallet = generateWallet(true); // Generate a SegWit wallet
console.log("Mnemonic:", wallet.mnemonic);
console.log("Address:", wallet.address);
console.log("Private Key:", wallet.privateKey);
```

### Fetch Address Information

```typescript
import { getAddressInfo } from './btc-sdk';

getAddressInfo("tb1q...")
    .then(info => console.log("Address Info:", info))
    .catch(err => console.error(err));
```

### Create a Transaction

```typescript
import { createTransaction } from './btc-sdk';

const mockUtxos = [
    { txid: "mock_txid_1", vout: 0, value: 100000 },
    { txid: "mock_txid_2", vout: 1, value: 50000 },
];

const rawTx = createTransaction(
    "sender_address",
    "sender_private_key",
    "recipient_address",
    120000, // Amount in satoshis
    5000,   // Fee in satoshis
    mockUtxos,
    true    // Use SegWit
);
console.log("Raw Transaction:", rawTx);
```

### Create a Multisig Address

```typescript
import { createMultisigAddress } from './btc-sdk';
import * as bitcoin from 'bitcoinjs-lib';

const pubkeys = [
    bitcoin.ECPair.makeRandom().publicKey,
    bitcoin.ECPair.makeRandom().publicKey,
];

const { address, redeemScript } = createMultisigAddress(pubkeys, 2);
console.log("Multisig Address:", address);
console.log("Redeem Script:", redeemScript.toString('hex'));
```

### Fetch Blockchain Data

#### Fetch Transaction Details

```typescript
import { getTransaction } from './btc-sdk';

getTransaction("transaction_id")
    .then(tx => console.log("Transaction Details:", tx))
    .catch(err => console.error(err));
```

#### Fetch Block Details

```typescript
import { getBlock } from './btc-sdk';

getBlock("block_hash")
    .then(block => console.log("Block Details:", block))
    .catch(err => console.error(err));
```

## Development

Run the TypeScript compiler to build the SDK:

```bash
npm run build
```

## License

This SDK is licensed under the MIT License.

