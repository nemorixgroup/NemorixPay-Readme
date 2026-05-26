# NemorixPay - Official document

<p align="left"></p>

<p align="left">
  <img src="https://github.com/nemorixpay/NemorixPay-Readme/blob/main/img/Logo%20Nemorix.png" width="400" title="NemorixPay logo">
</p>

## Subsection: Hedera integration

**Hedera SDKs**

Hedera offers official SDKs for Java, JavaScript, Go, Swift, C++, and Rust. For Flutter and Dart developers, **hedera_flutter_sdk** is the first native Flutter/Dart SDK for Hedera, built by Nemorix Group. It provides direct access to all Hedera services via gRPC without platform channels or backend workarounds. Read more details, [Hedera SDKs](https://docs.hedera.com/hedera/sdks-and-apis/sdks) on Hedera's official website.

**Wallet Application Development Guide**

Hedera provides documentation for building applications using its network services. This guide covers account creation, key management, token operations via HTS, and consensus messaging via HCS. Read more details, [Build on Hedera](https://docs.hedera.com/hedera/getting-started) on Hedera's official website.

**hedera_flutter_sdk**

The hedera_flutter_sdk, developed by Nemorix Group, is an open-source pure Dart library that provides APIs for building and signing transactions, as well as connecting directly to Hedera consensus nodes via gRPC. This SDK also supports Hedera Token Service (HTS) and Hedera Consensus Service (HCS). Read more details, [hedera_flutter_sdk](https://pub.dev/packages/hedera_flutter_sdk) on pub.dev.

Key Features:

* **Transaction Management**: Build, sign, and submit transactions to the Hedera network via gRPC.

* **HederaClient**: Connect to mainnet, testnet, or previewnet with a fluent builder pattern.

* **HTS Token Support**: The SDK includes support for Hedera Token Service (HTS), such as:

  * *Fungible Tokens*: Create, transfer, and manage fungible tokens including native USDC on Hedera.

  * *Non-Fungible Tokens*: Mint and transfer NFTs with native royalty and custom fee support.

  * *Native KYC*: Grant and revoke KYC on-chain; no anchor license required.

  * *Freeze and Pause*: Native asset control mechanisms for compliance use cases.

* **HCS Audit Logs**: Immutable on-chain transaction records via Hedera Consensus Service, satisfying FinCEN 5-year record retention requirements under the Bank Secrecy Act.

* **BIP-39 Mnemonics**: Native support for 12 and 24-word mnemonics in English and Spanish; the first Hedera SDK designed for LATAM users.

**Installation**:

To integrate hedera_flutter_sdk into your project, add the following dependency to your pubspec.yaml file:

```yaml
dependencies:
  hedera_flutter_sdk: ^1.0.0
```

**Note**: We need to ensure that Dart SDK environment is set to version *3.0.0* or higher and Flutter *3.10.0* or higher.

**Recent Updates**:

The latest release, version *0.0.3-dev*, includes 335 Dart classes generated from Hedera HAPI Protobuf definitions, base model classes (AccountId, TokenId, TransactionId, Hbar), HederaClient with testnet/mainnet/previewnet support, and HederaConstants with protocol-level values.

For comprehensive documentation, example usage, and to access the source code, visit the [hedera_flutter_sdk GitHub repository](https://github.com/nemorixgroup/hedera-flutter-sdk).

## Example: Create a new Account

### 📌 Steps to Create a Hedera Account on Mainnet

Each Hedera account has:

Account ID (e.g. 0.0.12345) → Used to receive funds.  
Private Key (ED25519 or ECDSA) → Used to sign transactions. (**Never share it!**)  

1️⃣ **Generate a Keypair and Mnemonic**

To generate a new wallet in Dart (Flutter) using hedera_flutter_sdk:

```dart
import 'package:hedera_flutter_sdk/hedera_flutter_sdk.dart';

void main() async {
  // Generate a 24-word mnemonic in Spanish (for LATAM users)
  final mnemonic = await Mnemonic.generate24(
    language: MnemonicLanguage.spanish,
  );
  print("Mnemonic: ${mnemonic.words.join(' ')}");

  // Derive private and public key from mnemonic
  final privateKey = await mnemonic.toPrivateKey();
  final publicKey = privateKey.publicKey;
  print("Public Key: ${publicKey.toString()}");
}
```
📌 **Store the mnemonic securely. It is the only way to recover your wallet.**

🔹 **Connect to Hedera Testnet**

```dart
// Connect to testnet using an existing operator account
final client = HederaClient.forTestnet()
    .setOperator(
      AccountId.fromString('0.0.12345'),
      PrivateKey.fromString('302e...'),
    );
```
🔹 **Free HBAR available at [portal.hedera.com](https://portal.hedera.com)**.

2️⃣ **Fund the New Account with at Least 1 HBAR** (*if Mainnet*)

A Hedera account requires a minimum balance to remain active on the network.

Here are several ways to fund the new account:

✅ **Option 1**: Transfer from an Exchange  
You can buy HBAR on an exchange (such as Binance, Coinbase, or Kraken) and send it to your *Account ID*.

✅ **Option 2**: Request HBAR from Another Account  
If you already have another Hedera account with a balance, you can send HBAR to the new account.

✅ **Option 3**: Use the Hedera Developer Portal  
On testnet, the Hedera Portal provides free HBAR for development and testing purposes.

3️⃣ **Verify That the Account is Created**

After funding the account, you can verify it using the Mirror Node REST API or HashScan explorer.

**_Example_**:

```dart
import 'package:hedera_flutter_sdk/hedera_flutter_sdk.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';

void main() async {
  final accountId = "0.0.12345";
  final url = '${HederaConstants.testnetMirrorNodeUrl}'
      '/api/v1/accounts/$accountId';

  final response = await http.get(Uri.parse(url));
  final data = jsonDecode(response.body);

  print("Account balance: ${data['balance']['balance']} tinybars");
  print("Account ID: ${data['account']}");
}
```
If the account exists and has a balance, it is active and ready to use.

4️⃣ **Use the Account to Send or Receive HBAR**

Once activated, you can use your account to send or receive payments on the Hedera network.

**_Example_**: Sending 10 HBAR to another account:

```dart
import 'package:hedera_flutter_sdk/hedera_flutter_sdk.dart';

void main() async {
  final client = HederaClient.forTestnet()
      .setOperator(
        AccountId.fromString('0.0.12345'),
        PrivateKey.fromString('302e...'),
      );

  final senderId = AccountId.fromString('0.0.12345');
  final receiverId = AccountId.fromString('0.0.67890');

  final txId = await CryptoTransferTransaction()
      .addHbarTransfer(senderId, Hbar(10).negated())
      .addHbarTransfer(receiverId, Hbar(10))
      .execute(client);

  final receipt = await txId.getReceipt(client);
  print("Transaction status: ${receipt.status}");
}
```

🔹 **Transfer USDC (HTS Fungible Token)**

```dart
final usdcTokenId = TokenId.fromString('0.0.456858'); // USDC on Hedera testnet

final txId = await TransferTransaction()
    .addTokenTransfer(usdcTokenId, senderId, -100)
    .addTokenTransfer(usdcTokenId, receiverId, 100)
    .execute(client);

print("USDC Transfer sent: ${txId.toString()}");
```

### 📌 Quick Summary

* Generate a Keypair and BIP-39 mnemonic (English or Spanish).
* Fund the account with HBAR from an exchange or the Hedera Portal (testnet).
* Verify that the account is active using the Mirror Node REST API or HashScan.
* Use the account to send/receive HBAR and HTS tokens (including USDC) on the Hedera network.

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
