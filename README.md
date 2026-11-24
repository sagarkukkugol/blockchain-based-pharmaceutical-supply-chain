# Blockchain-Based Pharmaceutical Supply Chain Management System

A blockchain-powered platform for improving transparency, traceability, and trust in the pharmaceutical supply chain. The system enables stakeholders to track medicine batches from manufacturing to final delivery, maintain a verifiable ownership history, and help consumers verify the authenticity of pharmaceutical products.

## Overview

The pharmaceutical supply chain involves multiple stakeholders, including manufacturers, transporters, distributors, and pharmacies. Traditional supply chain systems often rely on centralized records, making it difficult to maintain a consistent history of product movement and independently verify product information.

This project addresses these challenges through an Ethereum-based blockchain application. It uses Solidity smart contracts to manage pharmaceutical batches, ownership transfers, delivery updates, and transaction history. A React-based interface provides role-specific dashboards, while MetaMask enables users to connect their wallets and authorize blockchain transactions.

QR codes make batch verification accessible, and IPFS provides decentralized storage for shareable QR-code images.

## Objectives

- Improve transparency and traceability throughout the pharmaceutical supply chain.
- Maintain tamper-resistant records of pharmaceutical batches and ownership transfers.
- Provide role-based access for supply chain participants.
- Enable consumers to verify products using QR codes or batch identifiers.
- Monitor temperature conditions during pharmaceutical transportation.
- Maintain a verifiable history of batch-related activities.
- Provide a decentralized storage option for QR-code images using IPFS.

## Key Features

### 1. Role-Based Access and Dashboards

The platform supports different roles, each with specific responsibilities:

- **Admin:** Manages participants and assigns roles.
- **Manufacturer:** Registers pharmaceutical batches and provides product information.
- **Transporter:** Receives batches, records transportation information, and transfers ownership.
- **Distributor:** Manages batches received from transporters and transfers them to the next participant.
- **Pharmacy:** Receives batches, manages delivery status, and participates in product verification workflows.
- **Consumer:** Can verify pharmaceutical products and view their supply chain history without requiring a stakeholder account.

### 2. Blockchain-Based Batch Registration

Manufacturers can register pharmaceutical batches through the application.

Batch information is recorded through Solidity smart contracts, providing a consistent and verifiable record of product registration.

The system uses unique Batch IDs to identify individual batches, even when multiple batches belong to the same product.

### 3. Ownership Transfer and Tracking

The system supports the transfer of pharmaceutical batches between authorized supply chain participants.

Each ownership transfer is processed through the smart contract and recorded on the blockchain.

This provides a traceable history of:
- Previous and current ownership.
- Batch registration.
- Ownership changes.
- Delivery status updates.
- Transaction timestamps and blockchain references.

### 4. QR Code Generation and Product Verification

A QR code is generated for each registered pharmaceutical batch.

Consumers and other authorized users can scan the QR code to access the corresponding batch verification information.

The application supports:
- Batch-specific QR code generation.
- QR code downloading.
- Batch identification and verification.
- Access to the pharmaceutical batch history.

### 5. IPFS Integration

The application integrates with a locally running IPFS (Kubo) node to provide decentralized storage for QR-code images.

When a user chooses to save a QR code to IPFS:
1. The generated QR-code image is sent to the backend.
2. The backend communicates with the local IPFS node through its HTTP API.
3. IPFS stores the image and returns a Content Identifier (CID).
4. The application associates the CID with the corresponding batch.

QR codes can still be generated and downloaded without IPFS. IPFS is an additional storage option rather than a requirement for basic QR-code functionality.

### 6. Temperature Monitoring

The system includes temperature monitoring to support pharmaceutical cold-chain management.

Manufacturers can specify the acceptable temperature range for a batch. During transportation, temperature readings can be recorded and checked against the configured limits.

The system maintains information such as:
- Recorded temperature.
- Permissible temperature range.
- Whether the reading is within the permitted range.
- Recording participant.
- Recording timestamp.

Temperature records are managed through the backend rather than being stored directly in the smart contract.

### 7. Batch History and Transaction Records

The batch history module provides a timeline of important activities associated with a pharmaceutical batch.

It includes:
- Batch registration.
- Ownership transfers.
- Delivery status changes.
- User ratings.

Blockchain events provide transaction references, block numbers, and timestamps to help users trace the batch throughout its lifecycle.

### 8. Ratings and Consumer Feedback

The platform supports feedback from supply chain participants and consumers.

- Supply chain participants can rate the stakeholder from whom they received a batch.
- Consumers can submit product ratings after delivery.
- Consumer feedback can include a star rating and comments.
- Smart contract validation helps ensure that consumer ratings are submitted only for delivered batches.

## Technology Stack

| Component | Technologies |
|---|---|
| Frontend | React.js, Vite, JavaScript, HTML, CSS |
| Backend | Node.js, Express.js |
| Smart Contracts | Solidity |
| Blockchain Development | Hardhat |
| Blockchain Interaction | Ethers.js |
| Wallet Integration | MetaMask |
| Decentralized Storage | IPFS (Kubo) |
| QR Code Generation | QR Code library |
| Development Network | Hardhat Local Network |

## System Architecture

The application follows a layered architecture:

**1. User Interface Layer**

The React and Vite frontend provides role-based dashboards and interfaces for batch registration, ownership transfers, QR-code generation, and product verification.

**2. Application Layer**

The Node.js and Express backend handles application APIs and supporting data, including user account information, temperature records, and QR/IPFS metadata.

**3. Blockchain Layer**

Solidity smart contracts deployed using Hardhat manage roles, pharmaceutical batches, ownership transfers, delivery status, and relevant transaction records.

**4. Decentralized Storage Layer**

IPFS provides optional decentralized storage for QR-code images. The returned CID is associated with the corresponding batch.

MetaMask is used to connect user wallets and authorize blockchain transactions through Ethers.js.

## Project Workflow

1. A user registers through the application.
2. The backend processes the account information and provisions the user's blockchain wallet.
3. The appropriate role is assigned to the participant through the role-management mechanism.
4. The participant connects their wallet using MetaMask.
5. The manufacturer registers a pharmaceutical batch.
6. The smart contract validates and records the batch information.
7. A unique Batch ID and corresponding QR code are generated.
8. The batch moves through the supply chain as ownership is transferred between authorized participants.
9. Relevant ownership and delivery updates are recorded on the blockchain.
10. Temperature readings can be recorded during transportation.
11. The pharmacy receives the batch and updates its delivery status.
12. Consumers can scan the QR code or enter the Batch ID to verify the product and view its history.

## Getting Started

Follow these steps to set up the project locally.

### Prerequisites

Install the following software before running the application:

- Node.js and npm
- Git
- MetaMask browser extension
- Hardhat-compatible development environment
- IPFS Kubo (optional, for IPFS functionality)

### 1. Clone the Repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd pharmaceutical-supply-chain
```

### 2. Install Dependencies

Install dependencies in the frontend and blockchain/backend directories.

```bash
cd frontend
npm install
```

For the blockchain and backend dependencies:

```bash
cd ../blockchain
npm install
```

### 3. Start the Local Blockchain

Open a terminal in the blockchain directory and run:

```bash
npx hardhat node
```

This starts the local Hardhat blockchain network.

Keep this terminal running.

### 4. Deploy the Smart Contracts

Open another terminal in the blockchain directory:

```bash
npx hardhat run scripts/deploy.js --network localhost
```

Use the actual deployment script filename available in your repository if it differs.

After deployment, update the frontend contract address and ABI using the generated Hardhat artifacts as required.

### 5. Start the Backend Server

From the blockchain/backend directory, run the backend server using the command configured in your project.

For example:

```bash
node server.js
```

The backend development server runs at:

```text
http://127.0.0.1:4000
```

### 6. Start IPFS (Optional)

Install IPFS Kubo and initialize the node if it has not already been initialized.

```bash
ipfs init
ipfs daemon
```

Keep the IPFS daemon running when using the Save to IPFS functionality.

### 7. Start the Frontend

Open another terminal:

```bash
cd frontend
npm run dev
```

Open the local URL displayed by Vite in your browser.

### 8. Connect MetaMask

1. Install and open MetaMask.
2. Add the local Hardhat network.
3. Configure the network with the local RPC URL:

   `http://127.0.0.1:8545`

4. Set the Chain ID to `31337`.
5. Import a test account from the local Hardhat node when required.
6. Connect MetaMask to the application.

**Note:** Use only local development accounts and test funds. Never use real wallet private keys or mainnet funds for local testing.

## Testing

The project includes smart contract testing for important supply chain operations, including:

- Role assignment and access validation.
- Pharmaceutical batch registration.
- Unique batch identification.
- Ownership transfer.
- Input validation.
- Delivery status workflow.
- Transaction and batch history.

Run the available Hardhat tests from the blockchain directory:

```bash
npx hardhat test
```

## Data Storage Approach

The system uses different storage mechanisms depending on the type of information.

| Data | Storage |
|---|---|
| Participant roles | Blockchain |
| Pharmaceutical batch records | Blockchain |
| Ownership transfers | Blockchain |
| Delivery status | Blockchain |
| Relevant ratings and feedback | Blockchain |
| User account information | Backend JSON storage |
| Temperature records | Backend JSON storage |
| QR-code and IPFS metadata | Backend JSON storage |
| QR-code images saved through IPFS | IPFS |

This approach keeps important supply chain transactions verifiable on-chain while allowing supporting application data and files to be managed separately.

## Project Structure

The repository is organized around the frontend and blockchain/backend components.

```text
pharmaceutical-supply-chain/
│
├── frontend/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── ...
│
├── blockchain/
│   ├── contracts/
│   │   ├── SupplyChain.sol
│   │   └── Roles.sol
│   │
│   ├── scripts/
│   │   └── deploy.js
│   │
│   ├── test/
│   ├── artifacts/
│   ├── server.js
│   ├── package.json
│   └── ...
│
└── README.md
```

*The structure above illustrates the main components. Refer to the repository for the complete directory structure.*

## Security Considerations

- Blockchain transactions require wallet authorization through MetaMask.
- Smart contracts validate important supply chain operations.
- Role-based access helps restrict operations to authorized participants.
- Private keys and sensitive account information should never be committed to a public repository.
- Local development accounts should be used only for testing.
- The current implementation is intended as an academic prototype and requires additional security reviews before production deployment.

## Future Enhancements

Potential improvements include:

- Deployment to a suitable public or permissioned blockchain network.
- Integration with IoT sensors for automated temperature monitoring.
- Enhanced analytics and supply chain dashboards.
- Stronger authentication and account management.
- Improved notification and alert mechanisms.
- Production-grade decentralized file storage and access controls.
- Comprehensive security auditing and performance testing.

## Project Scope

This project demonstrates how blockchain technology, smart contracts, and decentralized storage can be combined to improve pharmaceutical supply chain traceability.

It is developed as an academic capstone project and uses a local blockchain development environment for implementation and testing.

## Contributors

Developed as a collaborative academic capstone project.

## License

This project is developed for academic and educational purposes. Add an appropriate open-source license to the repository if you intend to permit reuse or distribution.
