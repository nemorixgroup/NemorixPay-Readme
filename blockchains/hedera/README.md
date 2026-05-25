# Hedera Integration

## Overview

NemorixPay is evaluating Hedera as the primary blockchain 
for Phase 2, replacing the current Stellar integration. 
The decision is based on four key criteria: native KYC 
compliance, fixed transaction fees, mobile SDK availability, 
and environmental sustainability.

The mobile app will interact with the Hedera network using 
**hedera_flutter_sdk** - the first native Flutter/Dart SDK 
for Hedera, built by Nemorix Group - which provides essential 
tools for:

- **Account Management** - Creating and managing Hedera accounts
- **Transaction Handling** - Constructing, signing, and submitting 
  transactions to the Hedera network via gRPC
- **HBAR and Token Operations** - Querying balances, sending and 
  receiving HBAR and HTS tokens (USDC)
- **Native KYC** - Granting and revoking KYC on-chain via HTS; 
  no anchor license required
- **Audit Logs** - Immutable transaction records via Hedera 
  Consensus Service (HCS)

## Why Hedera for NemorixPay Phase 2

| Criteria | Stellar (Phase 1) | Hedera (Phase 2) |
|:---------|:-----------------|:----------------|
| KYC compliance | Anchor license ($300K+) | HTS native KYC; free |
| Transaction fee | Variable | $0.0001 fixed |
| Flutter SDK | Soneso stellar_flutter_sdk | hedera_flutter_sdk (Nemorix) |
| Finality | 3-5 seconds | 3-5 seconds |
| USDC support | Via anchor | Native HTS token |
| Audit log | Off-chain | HCS on-chain; immutable |
| Carbon footprint | Positive | Carbon-negative |

## Primary Goal - Phase 2

The primary goal of NemorixPay Phase 2 is to migrate the 
existing Flutter application to Hedera as the underlying 
network, enabling:

- **Native KYC compliance**: HTS token KYC eliminates the 
  need for a costly anchor license
- **Stablecoin transfers**: Sending and receiving USDC via 
  HTS on Hedera
- **Non-custodial wallet**: Users maintain full control of 
  private keys; BIP-39 mnemonics in English and Spanish
- **Immutable audit logs**: Every transaction recorded on HCS 
  for FinCEN compliance
- **Low-cost remittances**: Fixed $0.0001 fees enabling 
  micro-remittances for LATAM families

## Technology Stack

The Hedera integration uses the following packages:

```yaml
dependencies:
  # First native Flutter/Dart SDK for Hedera
  hedera_flutter_sdk: ^0.0.3-dev  # → v1.0.0 at launch
  
  # gRPC transport to Hedera consensus nodes
  grpc: ^5.1.0
  
  # Protobuf runtime (Hedera HAPI definitions)
  protobuf: ^6.0.0
  
  # BIP-39 mnemonics in English and Spanish
  bip39: ^1.0.6
  
  # ED25519 cryptography
  pointycastle: ^3.9.1
```

## Account Management

```dart
import 'package:hedera_flutter_sdk/hedera_flutter_sdk.dart';

// Connect to Hedera testnet
final client = HederaClient.forTestnet()
    .setOperator(
      AccountId.fromString('0.0.12345'),
      PrivateKey.fromString('302e...'),
    );

// Generate a new wallet with Spanish mnemonic
final mnemonic = await Mnemonic.generate24(
  language: MnemonicLanguage.spanish,
);

// Derive private key from mnemonic
final privateKey = await mnemonic.toPrivateKey();
final publicKey = privateKey.publicKey;
```

## Transaction Handling

```dart
// Transfer HBAR between accounts
final txId = await CryptoTransferTransaction()
    .addHbarTransfer(senderId, Hbar(10).negated())
    .addHbarTransfer(receiverId, Hbar(10))
    .execute(client);

// Wait for consensus and get receipt
final receipt = await txId.getReceipt(client);
print(receipt.status); // SUCCESS
```

## HTS Token Operations (USDC)

```dart
// Transfer USDC (HTS fungible token)
final txId = await TransferTransaction()
    .addTokenTransfer(usdcTokenId, senderId, -100)
    .addTokenTransfer(usdcTokenId, receiverId, 100)
    .execute(client);
```

## HCS Audit Log

```dart
// Record transaction on Hedera Consensus Service
final txId = await TopicMessageSubmitTransaction()
    .setTopicId(nemorixAuditTopicId)
    .setMessage(jsonEncode({
      'type': 'REMITTANCE',
      'sender': senderId.toString(),
      'receiver': receiverId.toString(),
      'amount': 100,
      'currency': 'USDC',
      'timestamp': DateTime.now().toIso8601String(),
    }))
    .execute(client);
```

## Network Configuration

```dart
// Mainnet (production)
final client = HederaClient.forMainnet();

// Testnet (development and testing)
// Free HBAR available at: https://portal.hedera.com
final client = HederaClient.forTestnet();

// Previewnet (upcoming features)
final client = HederaClient.forPreviewnet();
```

---

## Resources

- **hedera_flutter_sdk**: 
  [pub.dev](https://pub.dev/packages/hedera_flutter_sdk) | 
  [GitHub](https://github.com/nemorixgroup/hedera-flutter-sdk)
- **Hedera Developer Portal**: https://portal.hedera.com
- **Hedera Documentation**: https://docs.hedera.com
- **Mirror Node (testnet)**: https://testnet.mirrornode.hedera.com
- **HashScan Explorer**: https://hashscan.io

---

> **Status:** Under active evaluation for NemorixPay Phase 2.
> hedera_flutter_sdk is currently at v0.0.3-dev and will reach
> v1.0.0 by end of 2026.
