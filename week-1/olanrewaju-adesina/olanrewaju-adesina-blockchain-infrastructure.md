# Week 1 Day 2: Blockchain Infrastructure Research
**Student Name:** [Olanrewaju adesina]  
**Date:** [17-11-2025]  
**Tweet Link:** [Your Twitter thread link - add after posting]

---

## Part 1: Blockchain Infrastructure Research

### Blockchain 1: [Bitcoin]

#### Node Types
- Full node (archive / non-archive / pruned) — fully validates all blocks & transactions and stores the blockchain,Full nodes validate consensus rules, relay transactions/blocks and provide RPC to wallets and Pruned nodes validate all blocks but discard old block data to save storage. 

- SPV / light clients — do not store full chain, it rely on full nodes for block headers and proof-of-inclusion (useful for wallets). 

Mining nodes / miners (specialized) — nodes connected to ASIC rigs that create candidate blocks and broadcast them. Miners propose blocks and secure PoW.

#### Client Implementations
- Bitcoin Core — reference client, written in C++ (most widely used). 

- Bitcoin Knots — fork of Core with extra features, also C++. 

- btcd (Go), bcoin (JavaScript/Node) — alternative implementations for developers. 

#### Consensus Mechanism
Proof-of-Work (SHA-256 PoW): miners expend compute to solve difficulty puzzles; winner appends block and receives block reward + fees. Security comes from cost of producing valid PoW. 
Advantages: battle-tested, censorship resistance; Disadvantages: high energy, lower TPS & slower finality.

#### Block Validators
Miners (often in pools) propose blocks. Requirements: ASIC mining hardware (SHA-256 ASICs), cheap electricity, mining software and full-node client. 
Rewards: block subsidy (halving schedule) + transaction fees. 
Penalties: economic loss of electricity/costs; 51% attacks possible if attacker controls majority hashpower. No on-chain slashing mechanism

#### Performance Metrics
- Average block time: ~10 minutes (target). 

- Transaction finality: probabilistic; commonly 6 confirmations (~60 minutes) recommended for high-value transfers (finality not absolute; deeper confirmations reduce reorg risk). 

- Maximum TPS: ~3–7 TPS (practical limits of Bitcoin L1). Off-chain/Layer-2 (Lightning) handles many more payments.

#### Sources
- Bitcoin.org
- Investopedia

### Blockchain 2: [Solana]

#### Node Types
- Validator nodes — Validators run consensus (PoS + ordering via Proof of History), execute transactions (Sealevel parallel runtime), and maintain network liveness.

- RPC / Validator RPC nodes — RPC nodes provide APIs but may not stake/produce blocks. it also serve RPC endpoints for dApps, wallets; often separate from block-producing validators for performance.

- Archival / historical / snapshot nodes — store long-term ledger and account history for indexing & explorers. Geyser plugin-enabled nodes stream data to external DBs.

#### Client Implementations
- Agave (original Solana Labs client) — written in Rust (original/main client). 

- Firedancer — high-performance independent validator client developed by Jump Crypto, implemented in C / C++ to improve throughput & resilience. 

- Other clients / forks exist (e.g., Jito variants) and auxiliary clients (Mithril, others for lightweight use).

#### Consensus Mechanism
Proof of Stake (PoS) with Proof of History (PoH) for ordering (Solana’s PoH acts as a high-frequency cryptographic clock; Tower BFT provides finality). 
How it works: PoH creates an ordering, leaders produce blocks in slots, validators vote using a BFT protocol for finality. 
Advantages: very low latency and high throughput
Disadvantages: high hardware requirements can centralize validators and increases operational complexity.

#### Block Validators
Validators produce blocks (leaders are scheduled for slots). Requirements: significant stake delegation and high-performance hardware, no fixed small-stake minimum but practical barrier is high hardware + stake. 
Incentives: staking rewards (SOL inflationary rewards) + transaction fees; penalties include stake loss for equivocation (slashing can apply depending on protocol).

#### Performance Metrics
- Average block time: ~400 ms (slots ~400–600 ms). 

- Transaction finality: sub-second to seconds for most transactions; specific metrics vary (some sources cite ~12.8s for a conservative “finality” window depending on network conditions). 

- Maximum TPS: theoretical > 65,000 TPS (often quoted); real-world sustained TPS is much lower (hundreds–thousands depending on workloads and validator configs); Solana claims high throughput and design aimed at tens of thousands, and Firedancer aims to push performance further. Practical TPS depends on transaction composition and node setup. 

Note: Solana’s real-world TPS varies widely by block composition and validator hardware, official docs and recent validator reports are the best source for current live metrics. 


#### Sources
- neodyme.io
- solana.com

### Blockchain 3: [Ethereum]

#### Node Types
- Execution clients (EL) — handle EVM execution, transactions and state (formerly “Eth1 clients”). Examples: Geth, Erigon, Besu. 

- Consensus clients (CL) — handle PoS consensus & validator duties (Beacon chain). Examples: Prysm, Lighthouse, Teku, Nimbus, Lodestar. 

- Full nodes / Archive nodes / Light nodes — full nodes keep chain state; archive nodes keep full historical state for every block.

After the Merge, every Ethereum node typically runs two clients (an EL and a CL) to participate fully: EL executes and validates transactions; CL runs consensus (votes, proposer selection, finality).

#### Client Implementations
- Geth (Go) — most widely deployed execution client (written in Go). 

- Erigon (Go / optimized) — execution client focused on efficiency and resource usage (rewritten components). Erigon is an alternative optimized client. 

- Nethermind (C#) and Besu (Java) are other execution clients (enterprise-friendly features). Consensus clients include Prysm (Go), Lighthouse (Rust), Teku (Java), Nimbus (Nim), Lodestar (JS).

#### Consensus Mechanism
Proof of Stake (PoS) (post-Merge). Validators stake 32 ETH to run a validator (or use staking services/pools). Consensus is based on Gasper: LMD-GHOST (finality liveness) + Casper FFG (finality gadget). 
Blocks gain finality when 2/3+ of stake attest; typical finality time is ~2 epochs (~12.8 minutes) though user-facing confirmation guidance is often ~15 minutes (2–3 epochs). 
Advantages: far lower energy usage, higher validator participation; Disadvantages: new attack vectors (MEV, validator collusion), and different centralization trade-offs.

#### Block Validators
Validators propose and attest to blocks. Requirements: stake 32 ETH to run a validator (can use staking pools). Rewards: staking rewards (ETH issuance + fees depending on network conditions/MEV). Penalties: slashing for equivocation/double-signing or extended offline behavior (loss of stake)

#### Performance Metrics
- Average block time: 12–13 seconds per block (slot = 12 seconds). 

- Transaction finality: finality typically takes 2 epochs (12.8 minutes) to be finalized under normal conditions; user confirmations often recommend waiting 10–15 minutes for full finality. 

- Maximum TPS: Ethereum L1 practical TPS is in the low tens (varies with transaction complexity). Layer-2 rollups (Optimistic/ZK) are used to scale to hundreds-to-thousands+ TPS. (Exact L1 TPS varies by gas limits and transaction types.)


#### Sources
- eth2book.info
- https://consensys.io/blog/the-ethereum-2-0-beacon-chain-explained?utm_source=chatgpt.com



### Blockchain 4: [Binance Smart Chain Bsc]

#### Node Types
- Validator nodes — active set (originally 21) produce blocks and participate in consensus. 

- Full nodes — store the full history & validate blocks. 

- Archive nodes — store every historical state and are used for analytics/indexing. 

- Sentry nodes — optional front-line nodes protecting validators from direct public exposure (DDoS mitigation).

#### Client Implementations
- BNB Chain’s client is a fork of go-ethereum (geth) — codebase is a Geth fork (Go). Official repo: bnb-chain/bsc. 

- Alternative clients in the Ethereum ecosystem (e.g., Erigon forks for BSC) are used for archival/fast nodes in some setups. Languages: Go primarily for core BSC nodes (Geth-based); archival tooling often uses Erigon (Go) variants. 

Key differences: BSC clients are EVM-compatible and similar to Ethereum’s go-ethereum but with PoSA consensus & BNB-specific governance/features. Most popular: Geth-based BSC client (official) because it’s the reference and integrated with BNB governance

#### Consensus Mechanism
Proof of Staked Authority (PoSA) — hybrid of Delegated Proof-of-Stake / Proof-of-Authority: a limited validator set (historically 21) is elected by stake/delegation and takes turns producing blocks; PoSA enables short block times and low fees. Advantages: fast blocks, low fees; Disadvantages: more centralized validator set vs. fully permissionless PoS.

#### Block Validators
Validators in the active set produce blocks (rotating). 
Requirements: run a validator node (Geth-based), stake BNB (candidate / self-bonding numbers historically large — guides mention 10,000 BNB to be a candidate though effective active-set threshold varies). 
Rewards: transaction fees and potential staking rewards; 
penalties: slashing/economic penalties for misbehavior (double-signing) per PoSA logic.

#### Performance Metrics
- Average block time: historically ~3 seconds, but after 2025 upgrades (Lorentz & Maxwell / FastFinality) BNB Chain reduced block time targets (often cited 0.75s or even sub-second depending on upgrade specifics). Check BNB Chain docs for the exact current configured interval. 


- Transaction finality: with Fast Finality features, BNB Chain targets sub-second to a few seconds of finality (examples cite ~1.875s finality after upgrades). 

- Maximum TPS: BNB Chain reports high throughput metrics after upgrades; practical TPS varies with gas limits and upgrades — observational sources cite hundreds of TPS to a few thousand depending on gas configuration (Chainspect / BNB posts show real-world TPS in the hundreds). Upgrades claim potential for tens of thousands in improved configurations.


#### Sources
- docs.bnbchain.org
- https://github.com/bnb-chain/bsc?utm_source=chatgpt.com

### Comparison Table

| Blockchain | Consensus | Node Types | Main Client | Block Time | Validator Type |
|------------|-----------|------------|-------------|------------|----------------|
| [Bitcoin]  |Proof Of Work |   Full Node, Pruned Node, Mining Node, SPV/Light Client|     Bitcoin Core (C++)       |      ~10 mins      |        Miners (ASIC- based POW miners)    |                |
| [Ethereum] | Proof Of Stake|Execution Nodes, Consesus Nodes, Full Nodes, Archive Nodes, Light Clients| Geth + Lighthouse/prysm/Teku|~12 secs|Validators (32 ETH Stakers)|
| [Solana]   |   Proof Of History  | Validator Nodes, Full Nodes, Archival Nodes, Geyser Nodes| BNB Smart chain client | ~ 400–600 ms|    Validators (Stake-weighted block producers)|
| [Bnb]   |  Proof of staked Authority| Validator Nodes, Full Nodes, Archive Nodes, Sentry Nodes|BNB Smart Chain Client (Geth-based, Go)| 3 seconds|Validators (Delegated Staked Authority set) |

---

### Key Takeaways
[Write 3-5 key insights you learned from comparing these blockchains]
- Bitcoin prioritizes decentralization and security
- Solana and BNB Chain optimize for speed and throughput with sub-second or near-sub-second blocks but require more powerful hardware 
- Ethereum moderate block times and broad validator participation.
- Bitcoin PoW requires expensive ASIC hardware, limiting miners to specialized participants.
- BNB Chain relies on a small validator group, making the network fast but more centralized.
---

## Part 2: Distributed Ledger Technology vs Blockchain

### Introduction
[Your understanding of the topic]

### What is Distributed Ledger Technology (DLT)?
[Your explanation with detailed research]

### What Makes Blockchain Special?
[Explain the unique characteristics that define blockchain]

### Key Differences Between DLT and Blockchain
[Detailed technical comparison]

### Non-Blockchain Distributed Ledgers

#### DLT Example 1: [Name]
- **What it is:**
- **How it works:**
- **Key differences from blockchain:**
- **Use cases:**
- **Advantages over blockchain:**

#### DLT Example 2: [Name]
[Repeat structure]

#### DLT Example 3: [Name]
[Repeat structure]

---

### Comparison Table: Blockchain vs Non-Blockchain DLT

| Feature | Blockchain | Non-Blockchain DLT Example |
|---------|------------|---------------------------|
| Data Structure | | |
| Consensus Mechanism | | |
| Scalability | | |
| Energy Efficiency | | |
| Use Cases | | |

---

### Deep Analysis and Conclusions
[Your critical analysis on when to use blockchain vs other DLT solutions]

---

### All Sources and References
1. [Source 1]
2. [Source 2]
3. [Source 3]
[List all sources used in your research]

---

## Part 3: NFTs and Fungible Tokens - Digital Transformation

### Understanding Fungible Tokens
[Your detailed explanation]

### Understanding NFTs
[Your detailed explanation]

### How NFTs and Tokens Conquer the Physical World
[Your deep analysis on digital ownership revolution, transforming physical assets, new economic models, breaking physical limitations, and interoperability]

### Real-World Examples and Case Studies

#### Example 1: [Project Name]
- **What it is:**
- **How it works:**
- **Physical world connection:**
- **Impact:**
- **Token type:**
- **Blockchain:**

#### Example 2: [Project Name]
[Repeat structure]

#### Example 3: [Project Name]
[Repeat structure]

#### Example 4: [Project Name]
[Repeat structure]

#### Example 5: [Project Name]
[Repeat structure]

---

### Comparison Table: Physical vs Digital Ownership

| Feature | Physical Ownership | Digital Ownership (NFTs/Tokens) |
|---------|-------------------|--------------------------------|
| Ownership Verification | | |
| Transfer Speed | | |
| Transfer Cost | | |
| Storage | | |
| Divisibility | | |
| Global Accessibility | | |
| Fraud Prevention | | |
| Intermediaries | | |
| Programmable Features | | |

---

### Deep Analysis: The Future of Ownership
[Your critical analysis, vision, and insights]

---

**Twitter Thread:** [Add your tweet link here]