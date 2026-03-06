# Payvet

**Payvet** is a decentralized escrow platform built on BNBChain that enables secure, trustless payments between buyers and sellers. Funds are held in escrow via smart contracts and released automatically once agreed conditions are met — no intermediaries, no delays, no disputes left unresolved.

🌐 [payvet.app](https://payvet.app)

---

## Overview

Online transactions require trust between parties who may not know each other. This challenge is widespread across:

- Freelance marketplaces
- Peer-to-peer transactions
- Digital services
- E-commerce platforms
- Web3 marketplaces

Traditional escrow services depend on centralized intermediaries that introduce delayed payments, high fees, lack of transparency, platform censorship, and counterparty risk.

Payvet solves these problems using BNBChain smart contracts — funds are securely locked, verified, and released automatically according to predefined rules. The result is a **trustless, transparent, and programmable payment system** for the modern internet.

---

## Key Features

| Feature | Description |
|---|---|
| **Decentralized Escrow** | Funds are locked in a smart contract — no third party controls them |
| **Conditional Payments** | Programmable release conditions: delivery, milestones, time-locks, multi-step verification |
| **Dispute Resolution** | Contracts enter dispute mode with resolution mechanisms; decentralized arbitration planned |
| **Multi-party Verification** | Supports buyer + seller approval, escrow agent verification, and DAO arbitration |
| **Transparent Transactions** | All escrow activity is on-chain — fully immutable and verifiable |
| **Low Fees** | Built on BNBChain for affordable gas costs on both small and large payments |

---

## How It Works

```
Step 1 — Create Escrow      Buyer defines: amount, recipient, release conditions, expiry
Step 2 — Deposit Funds      Buyer locks funds in the smart contract
Step 3 — Execution          Seller delivers the agreed product or service
Step 4 — Verification       Conditions verified by buyer, both parties, or automated logic
Step 5 — Fund Release       Smart contract automatically releases funds to the seller
```

---

## Use Cases

- **Freelance Payments** — Clients lock funds before work begins; payment releases on completion
- **E-commerce** — Buyers purchase goods with funds held until delivery is confirmed
- **P2P Transactions** — Reduce fraud risk for individuals trading assets online
- **Web3 Marketplaces** — NFT platforms and decentralized exchanges can integrate Payvet for escrow
- **Service Marketplaces** — Milestone-based payments for long-term or consulting projects

---

## System Architecture

```
                +-----------------------+
                |       Frontend        |
                |   (Next.js / React)   |
                +----------+------------+
                           |
                           | Web3 Provider
                           |
                +----------v------------+
                |      Wallet Layer     |
                | (MetaMask / WalletConnect)
                +----------+------------+
                           |
                           | RPC Calls
                           |
                +----------v------------+
                |    BNBChain Network   |
                +----------+------------+
                           |
            +--------------+---------------+
            |                              |
+-----------v-----------+      +-----------v-----------+
|    Escrow Contract    |      |   Dispute Manager     |
|                       |      |                       |
| - Create Escrow       |      | - Trigger Disputes    |
| - Lock Funds          |      | - Arbitration Logic   |
| - Verify Conditions   |      | - Resolve Conflicts   |
| - Release Funds       |      |                       |
+-----------------------+      +-----------------------+
```

**Frontend Layer** — UI for creating and managing escrows with wallet connection and transaction interaction

**Wallet Layer** — User authentication and transaction signing via crypto wallets

**Smart Contract Layer** — Core escrow logic, fund custody, and dispute management

**Integration Layer** — APIs and SDKs for external developers

---

## Escrow State Machine

Every Payvet escrow follows a defined lifecycle:

```
    +-----------+
    |  Created  |   Escrow initialized, terms defined, no funds yet
    +-----------+
          |
          | Buyer deposits funds
          v
    +-----------+
    |  Funded   |   Funds locked in contract
    +-----------+
          |
          | Seller performs work
          v
    +-----------+
    | Completed |   Seller marks work as complete
    +-----------+
      /         \
     /           \
    v             v
+-----------+  +-----------+
| Released  |  |  Dispute  |   Buyer approves → funds sent to seller
+-----------+  +-----------+   Dispute raised → enters resolution
                    |
                    v
              +-----------+
              | Resolved  |   Arbitrator or resolution mechanism decides
              +-----------+
```

---

## Technology Stack

| Layer | Technologies |
|---|---|
| Blockchain | BNBChain |
| Smart Contracts | Solidity |
| Frontend | React, Next.js, Tailwind CSS |
| Web3 Libraries | wagmi, ethers.js, viem |
| Backend | Node.js, API services, Webhooks |
| Wallet Support | MetaMask, WalletConnect, BNBChain-compatible wallets |

---

## Installation

```bash
# Clone the repository
git clone https://github.com/payvet/payvet
cd payvet

# Install dependencies
npm install

# Run development server
npm run dev

# Compile smart contracts
npx hardhat compile

# Deploy to BNBChain testnet
npx hardhat run scripts/deploy.js --network bnbTestnet
```

### Project Structure

```
payvet/
├── contracts/
│   ├── Escrow.sol
│   └── DisputeManager.sol
├── frontend/
│   ├── components/
│   └── pages/
├── scripts/
│   └── deploy.js
├── test/
│   └── escrow.test.js
├── docs/
│   └── architecture.md
└── README.md
```

---

## Developer API

**Base URL:** `https://api.payvet.app`

### Endpoints

**Create Escrow**
```
POST /escrow/create
```
```json
{
  "buyer": "wallet_address",
  "seller": "wallet_address",
  "amount": "value",
  "token": "BNB or BEP20 token",
  "conditions": "escrow conditions",
  "expiry": "timestamp"
}
```
Response: `{ "escrowId": "12345", "status": "created" }`

**Deposit Funds**
```
POST /escrow/deposit
```
```json
{ "escrowId": "12345", "amount": "value" }
```

**Release Funds**
```
POST /escrow/release
```
```json
{ "escrowId": "12345", "approvedBy": "buyer_wallet" }
```

**Raise Dispute**
```
POST /escrow/dispute
```
```json
{ "escrowId": "12345", "reason": "description" }
```

---

## JavaScript SDK

```bash
npm install payvet-sdk
```

```javascript
import Payvet from "payvet-sdk"

const payvet = new Payvet({
  network: "bnb",
  rpcUrl: "https://bsc-dataseed.binance.org/"
})

// Create an escrow
const escrow = await payvet.createEscrow({
  buyer: walletAddress,
  seller: sellerAddress,
  amount: "1 BNB",
  conditions: "Delivery confirmed"
})

// Release funds
await payvet.releaseEscrow(escrow.id)
```

---

## Roadmap

- [x] **Phase 1** — Core escrow smart contract development
- [ ] **Phase 2** — Frontend web interface and wallet integrations
- [ ] **Phase 3** — Advanced dispute resolution system
- [ ] **Phase 4** — Developer SDK and third-party integrations
- [ ] **Phase 5** — Mainnet launch on BNBChain

---

## Security

Security is a top priority. Payvet's practices include:

- Smart contract audits
- Extensive automated testing
- Open-source transparency
- Bug bounty programs
- Continuous monitoring

> Always verify escrow conditions before depositing funds.

---

## Contributing

We welcome contributions from developers, researchers, and designers.

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Submit a pull request

Please ensure all contributions follow project coding standards.

---

## Contact

| Channel | Link |
|---|---|
| Website | [payvet.app](https://payvet.app) |
| Email | [team@payvet.app](mailto:team@payvet.app) |
| Telegram | [@Payvet](https://t.me/Payvet) |
