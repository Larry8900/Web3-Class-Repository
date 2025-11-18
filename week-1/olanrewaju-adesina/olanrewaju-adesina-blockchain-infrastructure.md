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
A Distributed Ledger Technology (DLT) is any protocol that maintains a replicated, shared ledger across multiple nodes without a single central authority; blockchain is one popular type of DLT that arranges records into an immutable, linearly chained sequence of blocks


### What is Distributed Ledger Technology (DLT)?
A distributed ledger is a database of transactions or states that is replicated and synchronized across multiple independent nodes in a network, where updates are made according to a protocol that the participant nodes follow instead of by a single central server. In short: shared, replicated records + network rules for agreement.

### What Makes Blockchain Special?
- Block + chain data structure — transactions are grouped into blocks; each block references the previous block via a cryptographic hash, forming a linear chain. This gives a simple, single canonical history (chain of blocks). 

- Global ordering — most blockchains enforce a single, global order of transactions (the chain) for everyone.

- Append-only immutability model — blocks are appended and older blocks are not rewritten (security provided by cryptographic linking + consensus). 

- Common consensus families — classic blockchain implementations use consensus like Proof-of-Work (Bitcoin) or Proof-of-Stake (modern Ethereum and many PoS chains) to secure that linear chain.

### Key Differences Between DLT and Blockchain
- Data structure

Blockchain (linear chain): blocks linked linearly by hashes. Simpler to reason about; reorgs (temporary forks) are possible and resolved by longest/heaviest chain rules. 

Non-blockchain DLTs: use Directed Acyclic Graphs (DAGs) (IOTA Tangle, Nano block-lattice), hashgraph event graphs (Hedera), agent-centric stores (Holochain), or notary / contract-specific ledgers (R3 Corda). These structures can allow parallel, non-linear confirmation paths and different ways to compute finality.

- Consensus & finality

Blockchain: consensus often yields probabilistic finality (PoW) or eventual/final finality (many PoS systems have explicit finality via BFT layers). Finality time varies. 

Non-blockchain DLTs: many provide fast or deterministic finality by design (e.g., hashgraph’s virtual voting gives fast Byzantine agreement; DAG designs can confirm transactions as soon as they're referenced by enough later transactions). Permissioned DLTs (Corda) use notaries to provide deterministic ordering/finality for a subset of transactions.

- Architecture & trust model

Blockchain: often designed for open permissionless environments (Bitcoin, Ethereum) with economic security assumptions (hashpower or stake). There are also permissioned blockchains (enterprise forks) that trade decentralization for governance control.

Non-blockchain DLTs: frequently designed for specialized or permissioned use cases (consortia, IoT, high-throughput micropayments) and may assume known, credentialed participants or use alternative selection mechanisms. Example: Corda shares transaction data only between counterparties and a notary — not globally broadcast.

### Non-Blockchain Distributed Ledgers

#### DLT Example 1: [IOTA]
- **What it is:** IOTA - The Tangle 
- **How it works:** Every new transaction must validate two previous transactions, the ledger is a Directed Acyclic Graph (DAG) rather than a linear chain. Consensus emerges as tips get confirmed by later transactions
- **Key differences from blockchain:**
- **Use cases:** IoT micropayments, machine-to-machine economics, zero-fee small transfers, offline/low-power environments.
- **Advantages over blockchain:** Higher theoretical parallelism (many transactions can be confirmed concurrently), low/no fees for micropayments, design optimized for massive numbers of small transactions. Also avoids grouping into blocks (lower latency in certain models).

#### DLT Example 2: [Hedera Hashgraph]
- **What it is:** Hedera is a permissioned governance model (governed by a council of enterprises) with an open public network. 
- **How it works:** Uses a gossip-about-gossip protocol and virtual voting to achieve Byzantine fault tolerant consensus. Each node gossips events (with cryptographic hashes) and the event graph enables nodes to infer votes without sending votes explicitly — producing fast, deterministic finality and strong throughput.
- **Key differences from blockchain:**
- **Use cases:** High-throughput tokenization, micropayments, enterprise record keeping where fast deterministic finality and governance are desire
- **Advantages over blockchain:** Very fast finality, high throughput and low latency, mathematically compact consensus (virtual voting), good for permissioned/enterprise contexts that want deterministic safety bounds.

#### DLT Example 3: [R3 Corda]
- **What it is:** Corda is notary-based and privacy-focused.
- **How it works:** Transactions are only shared with relevant counterparties; a notary service orders and attests to uniqueness (prevents double spends) for transactions that need global ordering. There is no global chain of blocks — instead, focused state transitions are recorded and notarized.
- **Key differences from blockchain:**
- **Use cases:** Inter-bank settlement, trade finance, KYC workflows — enterprise financial services where confidentiality and legal workflow integration matter.
- **Advantages over blockchain:** Strong privacy (no global broadcast), legal-workflow alignment, and lower overhead for transactions involving limited parties. It avoids broadcasting all state to all nodes, reducing data exposure and storage costs.

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