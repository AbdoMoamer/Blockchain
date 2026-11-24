# Blockchan: Blockchain Transaction Manager and Security Labs

A university project that implements a proof-of-work blockchain in Node.js, with a menu-driven CLI for managing wallets, miners, transactions and peer-to-peer nodes. The repository also contains the related cryptography lab exercises and a small Flask web application protected by a custom Web Application Firewall (WAF).

## Repository layout

| Folder | Contents |
| --- | --- |
| `A CLI-Based Blockchain Transaction Manager/` | Main project: blockchain core, wallets, miners, P2P networking, smart contracts, CLI |
| `Lab1/` | Node.js event-driven price tracker (`EventEmitter`, JSON file input) |
| `lab2/` | Blind-signature exercise (spy agency scenario) |
| `Lab3/` | Digital coin and bank exercise using blind signatures |
| `Waf/` | Flask demo app with a custom WAF (SQLi, XSS, LFI, RFI, command injection, path traversal rules) |
| `Screenshots_blockchain of all labs/` | Screenshots of lab results |

## Blockchain Transaction Manager

### Features

- **Proof-of-work mining.** SHA-256 block hashing with an adjustable difficulty (default 2 leading zeros) and a fixed mining reward (default 100 coins).
- **Signed transactions.** Wallets use secp256k1 key pairs (`elliptic`). Each transaction is hashed with SHA-256, signed with the sender's private key, and verified before it is accepted.
- **Balance checks.** A transaction is rejected if the sender's balance does not cover the amount plus their other pending transactions.
- **Pending pool.** Transactions wait in a pending list, are ordered oldest first, and up to 10 are included per mined block.
- **Wallet management.** Create, list, view and delete wallets. Key files are stored as JSON.
- **Miner management.** Create miners, assign them to clients, and track mining statistics. Rewards go to the assigned client, or to the miner if it is unassigned.
- **P2P networking.** Nodes talk over TCP sockets (Node.js `net`) with JSON messages, peer connections, broadcast, and automatic reconnect.
- **Blockchain explorer.** Look up the latest block, a block by hash or index, and a transaction by hash.
- **Statistics.** Per-user and network-wide balances, transaction volume, mining rewards and activity tables.
- **Smart contracts and messaging.** A simple contract manager, a name registry (DNS-style) and a messaging module.

### Tech stack

Node.js, `crypto` (SHA-256), `elliptic` (secp256k1), `crypto-js`, `qrcode`, Node.js `net` sockets.

### Installation

```bash
git clone https://github.com/AbdoMoamer/Blockchan.git
cd "Blockchan/A CLI-Based Blockchain Transaction Manager"
npm install
```

### Running

```bash
# Start a node (listens on port 6001) and open the CLI
npm start

# Or open the CLI directly
npm run cli
```

The main menu offers:

1. Client Management
2. Miner Management
3. Transaction Management
4. Network Management
5. Blockchain Explorer
6. System Statistics
7. Exit

### Typical workflow

1. Create wallets under **Client Management**.
2. Create a miner under **Miner Management** and assign it to a client.
3. Send a transaction under **Transaction Management** (it is signed and verified, then added to the pending pool).
4. Choose **Mine Pending Transactions** to create a block and collect the reward.
5. Inspect the result in **Blockchain Explorer** and **System Statistics**.
6. To test networking, start a second node and use **Network Management** to connect and broadcast.

## Web Application Firewall demo

```bash
cd Waf
pip install -r requirements.txt
python app.py
```

The Flask app uses a regex-based WAF with rate limiting, CSRF protection, input sanitisation (`bleach`) and an attack logger.

## Lab exercises

The `Lab1`, `lab2` and `Lab3` folders hold the course exercises in Node.js. `lab2` and `Lab3` need the `blind-signatures` package (`npm install blind-signatures`).

## Disclaimer

This is an educational project. The key files in the repository are demo data for local testing only and must not be used for real funds.

## Author

Abdelrahman Moamer, cybersecurity graduate and junior penetration tester.
LinkedIn: https://www.linkedin.com/in/abdelrahman-moamer-3583b8256/
