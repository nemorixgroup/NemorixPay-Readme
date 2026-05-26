# NemorixPay - Official document

<p align="left"></p>

<p align="left">
  <img src="https://github.com/nemorixpay/NemorixPay-Readme/blob/main/img/Logo%20Nemorix.png" width="400" title="NemorixPay logo">
</p>

## Blockchain Integrations

NemorixPay is designed to be blockchain-agnostic at the infrastructure
level. We evaluate each network based on five criteria: transaction cost,
finality speed, native compliance tools, mobile SDK availability, and
environmental impact.

The goal is to find the best blockchain infrastructure for low-cost,
regulated cross-border payments in Latin America; where millions of
families depend on remittances as a primary source of income.

### Evaluation Criteria

| Criteria                  | Weight | Why it matters                              |
|:--------------------------|:-------|:--------------------------------------------|
| Transaction cost          | 30%    | Directly impacts the fee charged to users   |
| Native compliance tools   | 25%    | KYC and AML without costly third parties    |
| Finality speed            | 20%    | Families need funds immediately             |
| Mobile SDK availability   | 15%    | Flutter-first development; no workarounds   |
| Environmental impact      | 10%    | Responsible infrastructure choice           |

### Networks Evaluated

| Network   | Flutter SDK                | Phase | Status               |
|:----------|:---------------------------|:------|:---------------------|
| Stellar   | Soneso stellar_flutter_sdk | 1     | Active integration   |
| Hedera    | hedera_flutter_sdk         | 1     | SDK in Development     |
| Algorand  | algorand_dart              | TBD   | Under evaluation     |

---

### Stellar Blockchain Integration

The mobile app will interact with the Stellar blockchain using the [Stellar Flutter SDK](https://github.com/Soneso/stellar_flutter_sdk), which provides essential tools for:

* **Account Management** - Creating and managing Stellar accounts.
* **Transaction Handling** - Constructing, signing, and submitting transactions to the Stellar network.
* **Balance & Payment Operations** - Querying balances, sending and receiving payments.
* **Soroban Smart Contracts** - (*Future scope*) Exploring contract deployment on Stellar’s Soroban.

📌 *Additional Notes*: The SDK documentation details [transaction signing and submission](https://github.com/Soneso/stellar_flutter_sdk/blob/master/soroban.md), ensuring compliance with Stellar's best practices.

More details on "[Stellar Integration](https://github.com/nemorixgroup/NemorixPay-Readme/tree/main/blockchains/stellar)" subsection.

### Hedera Blockchain Integration

The mobile app will interact with the Hedera network using 
[hedera_flutter_sdk](https://github.com/nemorixgroup/hedera-flutter-sdk), 
the first native Flutter/Dart SDK for Hedera, built by Nemorix Group. 
It provides essential tools for:

* **Account Management** - Creating and managing Hedera accounts with 
  ED25519 and ECDSA key support.
* **Transaction Handling** - Constructing, signing, and submitting 
  transactions to the Hedera network via gRPC.
* **Balance & Payment Operations** - Querying balances, sending and 
  receiving HBAR and HTS tokens (USDC).
* **Native KYC Compliance** - Granting and revoking KYC on-chain via 
  HTS; no anchor license required.
* **Audit Logs** - (*Future scope*) Immutable transaction records via 
  Hedera Consensus Service (HCS) for FinCEN compliance.

📌 *Additional Notes*: BIP-39 mnemonic support in English and Spanish 
is built in from day one; making hedera_flutter_sdk the first Hedera SDK 
designed for LATAM users.

More details on "[Hedera Integration](https://github.com/nemorixgroup/NemorixPay-Readme/tree/main/blockchains/hedera)" subsection.


### Algorand Blockchain Integration

The mobile app would interact with the Algorand network using
the [algorand_sdk](https://pub.dev/packages/algorand_dart),
a community Flutter/Dart SDK for Algorand. It provides
essential tools for:

* **Account Management** - Creating and managing Algorand 
  accounts with Ed25519 key support.
* **Transaction Handling** - Constructing, signing, and 
  submitting transactions to the Algorand network.
* **Balance and Payment Operations** - Querying balances, 
  sending and receiving ALGO and ASA tokens (USDC).
* **Smart Contracts** - *(Future scope)* Exploring AVM 
  smart contracts via PyTeal and ARC standards.

📌 *Additional Notes*: Algorand offers native USDC support 
via Circle and fixed fees of approximately $0.001 per 
transaction; making it a strong candidate for micro-remittances 
in LATAM markets.

More details on "[Algorand Integration](https://github.com/nemorixgroup/NemorixPay-Readme/tree/main/blockchains/algorand)" subsection.
