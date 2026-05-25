# NemorixPay - Official document

<p align="left"></p>

<p align="left">
  <img src="https://github.com/nemorixpay/NemorixPay-Readme/blob/main/img/Logo%20Nemorix.png" width="400" title="NemorixPay logo">
</p>


**Official website**: [nemorixpay.com](https://nemorixpay.com/)
#

## :star:Overview of NemorixPay Phase 1

<p align="left">NemorixPay will be a mobile-first payment platform designed to facilitate cross-border transactions between the U.S. and Latin America, starting with Mexico and Venezuela. The Phase 1 development focuses on delivering a seamless, secure, and low-cost solution for crypto-based remittances, leveraging blockchain technology to enable instant transactions with minimal fees. The mobile application will support stablecoins like USDC and XLM, providing users with a reliable alternative to traditional remittance services.</p>

### Goals and Scope of the Mobile Application

<p align="left">The primary goal of NemorixPay Phase 1 is to build a functional and user-friendly mobile application that enables:</p>

* **Crypto-to-crypto transactions**: Sending and receiving payments in USDC, XLM, and potentially other stablecoins.
* **Instant and low-cost transfers**: Using blockchain networks for fast and inexpensive transactions.
* **Non-custodial wallet support**: Users maintain full control of their funds without reliance on third-party intermediaries.
* **Basic user authentication and security measures**: Ensuring transactions are secure through encryption and authentication protocols.
* **Intuitive UI/UX design**: A mobile-first experience that is simple and accessible for both crypto-savvy users and newcomers.

<p align="left">The scope of Phase 1 is limited to:</p>

* Development of the mobile application for iOS and Android using Flutter.
* Integration with blockchain SDKs for remittance services.
* Secure local storage of transaction history and wallet keys (secure remote storage on servers as well).
* Basic KYC requirements for initial regulatory compliance.

<p align="left">Future phases will expand on this foundation by introducing fiat conversion, bank integrations, and additional compliance features.</p>

## :star: Progress Overview & Core Features (as of October 2025)

This section outlines the current state of the app, including key functionality, development progress, and upcoming priorities. Each feature is marked based on its implementation status in the roadmap, from initial proof-of-concept (PoC) to Minimum Viable Product (MVP).

| Functionality                     | Description                                                      | Status (PoC & MVP) |
| --------------------------------- | ---------------------------------------------------------------- | -------------------- |
| Account Creation                  | Create new accounts via the Flutter SDK.                 | ✅ (PoC)                   |
| Account Import                    | Import existing accounts using secret keys.              | ✅ (PoC)                   |
| Transaction Management            | Send, sign, and receive payments.         | ✅ (PoC)                   |
| Basic Auth login                  | Log in to the app using email and password credentials.          | ✅ (PoC)                   |
| Advanced Auth login               | Log in to the app using Google or Apple ID (OAuth).              | 🚧 (MVP)                   |
| Transaction History               | Allow users to view a complete list of their past transactions within the app. | 🚧 (MVP) |
| Basic Multilanguage Support       | App available in English and Spanish.                            | ✅ (PoC)                   |
| Local Private Key Custody         | Full local control and internal custody of public/private keys.  | ✅ (PoC)                   |
| Extended Multilanguage Support    | Add Portuguese and French.                                       | 🚧 (MVP)                  |
| Account Creation/Import | Create and import accounts.                | 🚧 🔥 (MVP)               |
| On/Off Ramps (Eg. Anchors)  | Eg. Connecting with Bitso for MXN ↔️ XLM/USDC deposits and withdrawals. | 🚧 🔥 (MVP)    |
| CoinGecko API                     | Integration with CoinGecko to gain access to real-time digital asset information.  | 🚧 (MVP)     |
| KYC (Know Your Customer)  | Integration with Didit.me to meet regulatory compliance and strengthen trust with users and partners.                                | 🔄 🛠️ 🔥 (MVP)                  |
| Security Enhancements             | Protect account using 2FA App, Biometric login, SMS, and/or Email)    | 🚧 (MVP)                  |
| Stablecoin Management             | Support for USDC and XLM.                                        | 🔄 (PoC & MVP)            |
| Smart Contracts (Soroban)         | Not used in V1, planned for future releases.                     | 🌟                   |
| Custodial Key Management       | Users allow the platform to securely store seed phrases and private/public keys, both locally and remotely (with encryption and backups).  | 🚧 🔥 (MVP)               |
| Non-Custodial Key Management       | Users retain full control of their seed phrases. The platform will provide local/remote secure storage options for public/private keys.  | 🚧 🔥 (MVP)               |
| Transparency and Auditability     | Open-source code and verifiable blockchain transactions.         | 🔄 (PoC & MVP)            |

### Status Legend

| Icon | Status        | Brief Description                                         |
| :--: | :------------ | :-------------------------------------------------------- |
|  🔄  | In Progress   | The functionality is currently under development.         |
|  🚧  | Pending       | Not yet started or scheduled for a future release.        |
|  🌟  | Future        | Planned for a later version.                              |
|   ✅  | Completed     | Implemented, tested, and working correctly.               |
|  🛠️ | Under Review  | Completed, but undergoing further adjustments or testing. |
|  🔥  | High Priority | Critical or top-priority feature on the roadmap.          |

**More details on** "[Technical Overview](https://github.com/nemorixpay/NemorixPay-Readme/tree/main/technical/README.md)".

## ⭐ KYC Feature

### Overview

The **KYC (Know Your Customer)** feature of NemorixPay implements a comprehensive identity verification system using modern technologies and robust architecture. This feature is essential for compliance with financial regulations and ensuring platform security.

**Key Features:**
- 🔐 Secure identity verification with external KYC provider
- 🏗️ Clean Architecture with BLoC state management
- 📱 WebView integration for seamless user experience
- 🧪 Comprehensive testing strategy
- 🚀 Scalable and maintainable codebase

**Technologies:** Flutter, BLoC, WebView, Firebase Functions, Secure Storage

**More details on** "[KYC Feature Documentation](https://github.com/nemorixpay/NemorixPay-Readme/tree/main/kyc/README.md)".

## :star:Initial Technology Stack

<p align="left">NemorixPay’s mobile application will be built with a modern technology stack optimized for security, scalability, and seamless integration with the Stellar blockchain. The selection of technologies ensures high performance, maintainability, and cross-platform support.</p>

### Core Technologies

* **Programming Language**: Dart
* **Framework**: Flutter (for cross-platform mobile development, Android & iOS)
* **State Management**: BLoC (Business Logic Component)
* **Initial Backend Infrastructure**: Firebase (authentication, database, and cloud functions)
* **Storage**: Secure Storage for sensitive data (e.g., user keys and credentials)
* **Networking**: HTTP & WebSocket for real-time data fetching and transaction updates
* **Cryptography**: Stellar SDK built-in cryptographic tools for signing transactions

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

### Stellar Blockchain Integration

The mobile app will interact with the Stellar blockchain using the [Stellar Flutter SDK](https://github.com/Soneso/stellar_flutter_sdk), which provides essential tools for:

* **Account Management** - Creating and managing Stellar accounts.
* **Transaction Handling** - Constructing, signing, and submitting transactions to the Stellar network.
* **Balance & Payment Operations** - Querying balances, sending and receiving payments.
* **Soroban Smart Contracts** - (*Future scope*) Exploring contract deployment on Stellar’s Soroban.

📌 *Additional Notes*: The SDK documentation details [transaction signing and submission](https://github.com/Soneso/stellar_flutter_sdk/blob/master/soroban.md), ensuring compliance with Stellar's best practices.

More details on "[Stellar Integration](https://github.com/nemorixgroup/NemorixPay-Readme/tree/main/blockchains/stellar)" subsection.

## ⭐System Architecture

The application follows the principles of **Clean Architecture**, promoting a clear separation between the *presentation*, *domain*, and *data layers*. This approach enhances maintainability and scalability.

* **Presentation Layer**: Manages the UI components and user interactions. Utilizes the BLoC pattern to handle state management, ensuring a reactive and streamlined user experience.
* **Domain Layer**: Contains the core business logic and entities. Defines use cases that encapsulate application-specific business rules.
* **Data Layer**: Responsible for data retrieval from external sources, such as the Stellar network, and local storage. Implements repositories that abstract the data sources, providing a clean API to the domain layer.

### **BloC Pattern for State Management in Flutter**

The BloC (_Business Logic Component_) pattern is a powerful state management approach in Flutter that promotes separation of concerns by managing business logic and UI separately. It utilizes **Streams** and **Sinks** to handle state changes reactively, making applications more scalable and testable.

**How it Works**

* **Events**: The UI triggers events when a user interacts with the app.
* **Bloc**: The event is processed within the Bloc, where business logic executes and determines the new state.
* **States**: The UI listens to state changes and updates accordingly.

**Key Benefits**
* Clear separation of UI and logic, enhancing maintainability.
* Reactive programming, improving performance and responsiveness.
* Scalability, making it suitable for complex applications.

Flutter provides the [flutter_bloc](https://pub.dev/packages/flutter_bloc) package, which simplifies the implementation of the BloC pattern and integrates seamlessly with widgets.

More details on "[System Architecture](https://github.com/nemorixpay/NemorixPay-Readme/blob/main/architecture/architecture.md)" subsection.

### Security Considerations

Security is paramount in the design of NemorixPay. Key measures include:

* **Data Encryption**: Sensitive data is encrypted both in transit and at rest.
* **Authentication**: Implementation of robust authentication mechanisms to ensure authorized access.
* **Error Handling**: Comprehensive error handling to manage exceptions and maintain application stability.

By adhering to these initial architectural principles and leveraging the capabilities of the Stellar network, NemorixPay aims to deliver a robust and user-centric platform for cross-border cryptocurrency transactions.

More details on "[Security](https://github.com/nemorixpay/NemorixPay-Readme/blob/main/security/README.md)" subsection.

In terms of compliance, **NemorixPay** is in the process of registering as a **Money Services Business** (MSB) with **FinCEN**.

This registration strengthens our commitment to regulatory compliance, enhances transparency, and builds trust with both users and third-party partners. As an MSB, NemorixPay will operate under federal guidelines that help ensure secure handling of digital assets and responsible financial operations. 

More details on "[MSB](https://github.com/nemorixpay/NemorixPay-Readme/blob/main/msb/README.md)" subsection.

### Testing & Quality Assurance

Mobile Testing & QA ensures that a mobile application is functional, reliable, secure, and user-friendly before and after release. It involves testing on different devices, OS versions, screen sizes, and network conditions to guarantee a smooth user experience.

More details on "[Testing & Quality Assurance](https://github.com/nemorixpay/NemorixPay-Readme/blob/main/testing/testing.md)" subsection.

## ⭐ Basic Flowcharts

These basic diagrams outline the user journey from opening the app to accessing the dashboard, including authentication checks, processing transactions, user settings, and some more options.

More details on "[Basic flowcharts](https://github.com/nemorixpay/NemorixPay-Readme/blob/main/flowcharts/flowcharts.md)"

## ⭐User Experience (UX)

The initial UX mockups are presented here. You can view the complete design (both dark and light mode) in the "[Design](https://github.com/nemorixpay/NemorixPay-Readme/blob/main/design/README.md)" subsection.

<p align="center">
  <img src="https://github.com/nemorixpay/NemorixPay-Readme/blob/main/img/design/splash_screen.jpg" width="200" title="NemorixPay logo">
  <img src="https://github.com/nemorixpay/NemorixPay-Readme/blob/main/img/design/login_empty_state.jpg" width="200" title="NemorixPay logo">
  <img src="https://github.com/nemorixpay/NemorixPay-Readme/blob/main/img/design/transaction_history.jpg" width="200" title="NemorixPay logo">
</p>


## :star:Overview of NemorixPay Phase 2 (Future!)

**Phase 2** should expand NemorixPay beyond mobile, offering a secure, scalable, and intuitive web solution for both individual users and merchants. This phase ensures a seamless experience across platforms while leveraging **Stellar’s blockchain** capabilities for fast and low-cost transactions.

### 🎯 Objective:  
Develop a web-based platform that mirrors and extends NemorixPay’s mobile capabilities, providing users with additional flexibility to manage their finances, make payments, and access financial services from a desktop or browser.

### 🔜 Next Steps for Phase 2:

* **Define Tech Stack**: Will we use React, Next.js, or another framework?
* **Design Wireframes**: Ensure UI/UX is aligned with mobile design.
* **Set Up Backend**: Prepare APIs & Horizon connections for blockchain interactions.
* **Security Audit**: Plan end-to-end encryption & secure login methods.
* **Beta Testing**: Release a limited web beta for early adopters & businesses.
