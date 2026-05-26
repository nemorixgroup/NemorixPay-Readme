# NemorixPay - Official document

<p align="left"></p>

<p align="left">
  <img src="https://github.com/nemorixpay/NemorixPay-Readme/blob/main/img/Logo%20Nemorix.png" width="400" title="NemorixPay logo">
</p>

## Subsection: Algorand integration

**Algorand SDKs**

Algorand offers a variety of SDKs for interacting with its network, including JavaScript, Python, Go, Java, and Dart SDKs. These SDKs allow developers to build and sign transactions, as well as connect to and query Algod and Indexer, Algorand's primary APIs. Read more details, [Algorand SDKs](https://developer.algorand.org/docs/sdks/) on Algorand's official website.

**Wallet Application Development Guide**

Algorand provides a guide for developing wallet applications using its SDK. This guide covers topics such as SDK installation, client setup, account creation, and the fundamentals of Algorand Standard Assets (ASA) and atomic transfers. Read more details, [Build on Algorand](https://developer.algorand.org/docs/get-started/basics/why_algorand/) on Algorand's official website.

**Algorand Dart SDK**

The Algorand Dart SDK, developed by the community, is an open-source Dart library that provides APIs for building and signing transactions, as well as connecting to and querying Algod and Indexer nodes. This SDK also supports AVM smart contracts via PyTeal and TEAL. Read more details, [algorand_dart](https://pub.dev/packages/algorand_dart) on pub.dev.

Key Features:

* **Transaction Management**: Build, sign, and submit transactions to the Algorand network.

* **Algod and Indexer Interaction**: Connect to Algod nodes to submit transactions and query network state; use Indexer to search historical data.

* **ASA Support**: The SDK includes support for Algorand Standard Assets (ASA), such as:

  * *Fungible Tokens*: Create, transfer, and manage fungible tokens including USDC on Algorand.

  * *Non-Fungible Tokens*: Mint and transfer NFTs following ARC-3 and ARC-69 standards.

  * *Atomic Transfers*: Execute multiple transactions atomically; all succeed or all fail.

  * *Clawback and Freeze*: Native asset control mechanisms for compliance use cases.

* AVM Smart Contracts: The SDK supports AVM smart contracts (stateful and stateless) via TEAL and PyTeal, allowing deployment and invocation of contracts on Algorand.

**Installation**:

To integrate the Algorand Dart SDK into your project, add the following dependency to your pubspec.yaml file:

```yaml
dependencies:
  algorand_dart: ^2.0.0
```

**Note**: We need to ensure that Dart SDK environment is set to version *3.0.0* or higher.

**Recent Updates**:

The latest release introduces support for ARC-4 ABI encoding and enhanced support for inner transactions in smart contracts.

For comprehensive documentation, example usage, and to access the source code, visit the [algorand_dart pub.dev page](https://pub.dev/packages/algorand_dart).

## Example: Create a new Account

### 📌 Steps to Create an Algorand Account on Mainnet

Each Algorand account has:

Public Key (Address) → Used to receive funds.  
Private Key (Mnemonic) → Used to sign transactions. (**Never share it!**)  

1️⃣ **Generate a new Account (Public Key and Mnemonic)**

To generate a new account in Dart (Flutter) using the Algorand SDK:

```dart
import 'package:algorand_dart/algorand_dart.dart';

void main() async {
  final account = await Account.random();
  print("Public Key (Address): ${account.publicAddress}");
  print("Mnemonic: ${account.seedPhrase.join(' ')}");
}
```
📌 **Store the mnemonic securely. It is the only way to recover your account.**

🔹 **Create and fund a new account on Testnet**

```dart
final algorand = Algorand(
  algodClient: AlgodClient(apiUrl: AlgoExplorer.TESTNET_ALGOD_API_URL),
);

// Create a random account
final account = await Account.random();

// Fund the account using the Algorand Testnet Dispenser
// Visit: https://dispenser.testnet.aws.algodev.network/
print("Fund this address: ${account.publicAddress}");
```
🔹 **You can play in testnet using the Algorand Dispenser**.

2️⃣ **Fund the New Account with at Least 0.1 ALGO** (*if Mainnet*)

An Algorand account requires a minimum balance of 0.1 ALGO to be active on the network.

Here are several ways to fund the new account:

✅ **Option 1**: Transfer from an Exchange  
You can buy ALGO on an exchange (such as Binance, Kraken, or Coinbase) and send it to your *public address*.

✅ **Option 2**: Request ALGO from Another Account  
If you already have another Algorand account with a balance, you can send 0.1 ALGO to the new address.

✅ **Option 3**: Use a Ramp or On-ramp Provider  
Some platforms allow you to convert fiat money into ALGO and send it directly to an Algorand address.

3️⃣ **Verify That the Account is Created**

After funding the account, you can check if it has been activated by querying the Algod node.

**_Example_**:

```dart
import 'package:algorand_dart/algorand_dart.dart';

void main() async {
  final algorand = Algorand(
    algodClient: AlgodClient(
      apiUrl: AlgoExplorer.MAINNET_ALGOD_API_URL,
    ),
  );

  final address = "YOUR_PUBLIC_ADDRESS_HERE";
  final accountInfo = await algorand.getAccountByAddress(address);

  print("Account balance: ${accountInfo.amount} microALGO");
  print("Account status: ${accountInfo.status}");
}
```
If the account exists and has a balance, it is active and ready to use.

4️⃣ **Use the Account to Send or Receive ALGO**

Once activated, you can use your account to send or receive payments on the Algorand network.

**_Example_**: Sending 1 ALGO to another address:

```dart
import 'package:algorand_dart/algorand_dart.dart';

void main() async {
  final algorand = Algorand(
    algodClient: AlgodClient(
      apiUrl: AlgoExplorer.MAINNET_ALGOD_API_URL,
    ),
  );

  final account = await Account.fromSeedPhrase(
    "YOUR_MNEMONIC_HERE".split(' '),
  );

  final txId = await algorand.sendPayment(
    account: account,
    recipient: AlgorandAddress.fromAlgorandAddress(
      address: "DESTINATION_ADDRESS_HERE",
    ),
    amount: Algo.toMicroAlgos(1),
  );

  print("Transaction sent: $txId");
}
```

🔹 **Transfer USDC (ASA) on Algorand**

```dart
// USDC Asset ID on Algorand Mainnet: 31566704
final usdcAssetId = 31566704;

final txId = await algorand.assetManager.transfer(
  account: senderAccount,
  assetId: usdcAssetId,
  recipient: AlgorandAddress.fromAlgorandAddress(
    address: "DESTINATION_ADDRESS_HERE",
  ),
  amount: 1000000, // 1 USDC (6 decimals)
);

print("USDC Transfer sent: $txId");
```

### 📌 Quick Summary

* Generate a new Account (Public Key and Mnemonic).
* Fund the account with at least 0.1 ALGO from an exchange or another account.
* Verify that the account is active by checking it on the Algod node.
* Use the account to send/receive ALGO and ASA tokens (including USDC) on the Algorand network.
