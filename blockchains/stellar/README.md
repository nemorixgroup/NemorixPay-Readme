# NemorixPay - Official document

<p align="left"></p>

<p align="left">
  <img src="https://github.com/nemorixpay/NemorixPay-Readme/blob/main/img/Logo%20Nemorix.png" width="400" title="NemorixPay logo">
</p>

## Subsection: Stellar integration

**Stellar SDKs**

Stellar offers a variety of SDKs for interacting with its network, including JavaScript, Python, Go, Flutter, and Rust SDKs. These SDKs allow developers to build and sign transactions, as well as connect to and query Horizon, Stellar’s API. Read more details, [Stellar SDKs](https://developers.stellar.org/docs/tools/sdks) on Stellar official website.

**Wallet Application Development Guide**

Stellar provides a guide for developing wallet applications using its Wallet SDK. This guide is available for multiple programming languages, including TypeScript, Kotlin, and Flutter (Dart). It covers topics such as SDK installation, client setup, and the fundamentals of Stellar and Anchor. Read more details, [Build a Wallet with the Wallet SDK](https://developers.stellar.org/docs/category/build-a-wallet-with-the-wallet-sdk) on Stellar official website.

**Stellar Flutter SDK**

The Stellar Flutter SDK, developed by Soneso, is an open-source Dart library that provides APIs for building and signing transactions, as well as connecting to and querying Horizon. This SDK also supports Soroban, Stellar’s smart contract platform. It allows developers to deploy and invoke smart contracts using the SorobanServer class, which connects to a Soroban-RPC server. Read more details, [Stellar Flutter SDK](https://github.com/Soneso/stellar_flutter_sdk) on Soneso's GitHub repository.

Key Features:

* **Transaction Management**: Build, sign, and submit transactions to the Stellar network.

* **Horizon Interaction**: Connect to Horizon servers to query network data and submit transactions.

* **SEP Protocol Support**: The SDK includes support for various Stellar Ecosystem Proposals (SEPs), such as:

  * *SEP-0002* (Federation): Resolve Stellar addresses, account IDs, and transaction IDs using the federation protocol. 

  * *SEP-0011* (Txrep): Convert transaction envelopes to a human-readable format and vice versa. 

  * *SEP-0012* (KYC): Manage customer information, including fetching required fields, uploading data, and verification processes. 

  * *SEP-0006* (Transfer): Handle deposit and withdrawal operations with anchors. 

* Soroban Smart Contracts: The SDK offers experimental support for Soroban smart contracts, allowing deployment and invocation of contracts via the SorobanServer class.

**Installation**:

To integrate the Stellar Flutter SDK into your project, add the following dependency to your pubspec.yaml file:

```
dependencies:
  stellar_flutter_sdk: ^1.9.2
```

**Note**: We need to ensure that Dart SDK environment is set to version *2.17.0* or higher. 

**Recent Updates**:

The latest release, version *1.9.2*, introduces experimental support for Soroban passkeys and enhances SEP-12 compliance by adding support for post and get customer file endpoints. 

For comprehensive documentation, example usage, and to access the source code, visit the [Stellar Flutter SDK GitHub repository](https://github.com/Soneso/stellar_flutter_sdk).

## Example: Create a new Account

### 📌 Steps to Create a Stellar Account on Mainnet

Each Stellar account has:

Public Key (Address) → Used to receive funds.  
Private Key (Secret Key) → Used to sign transactions. (**Never share it!**)  

1️⃣ **Generate a Keypair (Public and Private Key)**

To generate a Keypair in Dart (Flutter) using the Stellar SDK:  

```dart
import 'package:stellar_flutter_sdk/stellar_flutter_sdk.dart';

void main() {
  KeyPair keyPair = KeyPair.random();
  print("Public Key (Address): ${keyPair.accountId}");
  print("Secret Key: ${keyPair.secretSeed}");
}
```
📌 **Store these keys securely**.  

 🔹 **Create and fund a new account on Testnet**

```dart
StellarSDK sdk = StellarSDK.TESTNET;

// Create a random key pair for our new account.
KeyPair keyPair = KeyPair.random();

// Ask the Friendbot to create our new account in the stellar network (only available in testnet).
bool funded = await FriendBot.fundTestAccount(keyPair.accountId);

// Load the data of the new account from stellar.
AccountResponse account = await sdk.accounts.account(keyPair.accountId);
```
🔹 **You can play in testnet**. 

2️⃣ **Fund the New Account with at Least 1 XLM** (*if Mainnet*)

A Stellar account does not exist on the blockchain until it receives at least 1 XLM.

Here are several ways to fund the new account:

✅ **Option 1**: Transfer from an Exchange  
You can buy 1 XLM or more on an exchange (such as Binance, Kraken, or Coinbase) and send it to your *public key* (address).

✅ **Option 2**: Request 1 XLM from Another Account  
If you already have another Stellar account with a balance, you can send 1 XLM to the new address.

✅ **Option 3**: Use a Stellar Anchor  
Some platforms allow you to convert fiat money into XLM and send it to a Stellar address.

3️⃣ **Verify That the Account is Created**

After sending 1 XLM, you can check if the account has been activated by querying Horizon (Stellar’s API server).

**_Example_**:

```dart
import 'package:stellar_flutter_sdk/stellar_flutter_sdk.dart';

void main() async {
  StellarSDK sdk = StellarSDK.PUBLIC; // Connect to mainnet
  String newAccountId = "YOUR_PUBLIC_KEY_HERE";

  AccountResponse? account = await sdk.accounts.account(newAccountId);

  if (account != null) {
    print("Account successfully created. Balance: ${account.balances[0].balance} XLM");
  } else {
    print("The account has not been activated yet.");
  }
}
```  
If the account exists, it means it has been activated and is ready to use.

4️⃣ **Use the Account to Send or Receive XLM**

Once activated, you can use your account to send or receive payments on the Stellar network.

**_Example_**: Sending 0.5 XLM to another address:

```dart
void sendPayment() async {
  StellarSDK sdk = StellarSDK.PUBLIC;

  String senderSecret = "YOUR_SECRET_KEY_HERE";
  String receiverPublic = "DESTINATION_ADDRESS_HERE";

  KeyPair senderKeyPair = KeyPair.fromSecretSeed(senderSecret);
  AccountResponse senderAccount = await sdk.accounts.account(senderKeyPair.accountId);

  Transaction transaction = TransactionBuilder(senderAccount)
    .addOperation(PaymentOperationBuilder(receiverPublic, Asset.NATIVE, "0.5").build())
    .build();

  transaction.sign(senderKeyPair, sdk.network);

  SubmitTransactionResponse response = await sdk.submitTransaction(transaction);
  print("Transaction sent: ${response.hash}");
}
```

🔹 Another Create Account Operation  
```
StellarSDK sdk = StellarSDK.TESTNET;

// Build a key pair from the seed of an existing account. We will need it for signing.
KeyPair existingAccountKeyPair = KeyPair.fromSecretSeed("SAPS66IJDXUSFDSDKIHR4LN6YPXIGCM5FBZ7GE66FDKFJRYJGFW7ZHYF");

// Existing account id.
String existingAccountId = existingAccountKeyPair.accountId;

// Create a random keypair for a new account to be created.
KeyPair newAccountKeyPair = KeyPair.random();

// Load the data of the existing account so that we receive it's current sequence number.
AccountResponse existingAccount = await sdk.accounts.account(existingAccountId);

// Build a transaction containing a create account operation to create the new account.
// Starting balance: 10 XLM.
Transaction transaction = new TransactionBuilder(existingAccount)
    .addOperation(new CreateAccountOperationBuilder(newAccountKeyPair.accountId, "10").build())
    .build();

// Sign the transaction with the key pair of the existing account.
transaction.sign(existingAccountKeyPair, Network.TESTNET);

// Submit the transaction to stellar.
await sdk.submitTransaction(transaction);

// Load the data of the new created account.
AccountResponse newAccount = await sdk.accounts.account(newAccountKeyPair.accountId);
```

### 📌 Quick Summary

* Generate a Keypair (Public and Private Key).
* Send at least 1 XLM to the Public Key from an exchange or another account.
* Verify that the account is created by checking it on Horizon.
* Use the account to send/receive XLM on the Stellar network.
