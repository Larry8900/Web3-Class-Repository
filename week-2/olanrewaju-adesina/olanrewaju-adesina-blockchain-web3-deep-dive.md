# Week 2: Blockchain & Web3 Deep Dive Research (Day 1-3)
**Student Name:** [Olanrewaju adesina]  
**Date:** [20-11-2025]  
**Tweet Link:** [Your Twitter thread link - add after posting]

---

## Part 1: Consensus Mechanisms Deep Dive

### Proof of Work (PoW) Analysis
How PoW works (step-by-step)

- Collect transactions: Nodes gather pending transactions into a candidate block.

- Compute proof (mining): Miners repeatedly change a nonce or other block fields and compute the block’s hash until they find a hash that meets the network’s target difficulty (i.e., the hash is numerically below a target). That hash is the PoW.

- Broadcast the block: The successful miner broadcasts the block to peers.

- Verify: Other nodes validate transactions and the PoW quickly by hashing once — cheap to verify, expensive to find.

- Append & continue: Nodes append the block to their chain and miners start on the next block.

- Difficulty adjustment: The protocol periodically adjusts the difficulty so blocks are produced at the target interval (e.g., Bitcoin ~10 minutes). If blocks come too fast, difficulty rises; if too slow, it falls.

Security model

How PoW prevents attacks

- Work cost: To rewrite history you must re-do the required computational work for a chain portion and outrun the honest chain — expensive in hardware, energy, and time.

- Economic disincentives: Honest mining yields predictable rewards; attacking puts your investment at risk because an attack can reduce coin value and your future reward stream.

Real-world examples 
- Bitcoin
- Ethereum classic, older coins and many altcoins

Advantages

- Battle-tested security — Bitcoin’s PoW is the most tested large-scale example.

- Simple safety model — security tied to physical resources (energy + hardware).

- Censorship resistance — widely distributed miners can be hard to coordinate against.

Disadvantages

- Energy intensive — substantial electricity use, environmental concerns (though actual impact depends on energy sources).

- Centralization pressure — economies of scale (ASIC manufacturers, large pools, cheap electricity) can concentrate mining power.

- Throughput & latency — scaling usually requires layer-2 systems; base layer throughput is limited.

### Proof of Stake (PoS) Analysis
[ How PoS works (step-by-step)

- Stake collateral: Participants lock up native tokens (stake) in a protocol contract to become validators.

- Validator selection: The protocol pseudo-randomly selects validators (or committees) to propose and attest (vote) on blocks. Selection weight is often proportional to stake size, possibly with randomness and shuffling to reduce predictability.

- Propose & attest: A selected validator proposes a block; other validators attest to it. The protocol aggregates attestations into finality votes.

- Finality: PoS designs often include a finality gadget (e.g., Casper FFG on top of LMD-GHOST in Ethereum) — once a block is finalized, it can’t be reverted except under extreme conditions.]

Security model

How PoS prevents attacks

- Economic stake at risk: To attack, an actor must acquire/control a large share of stake — they risk losing that stake to slashing and value erosion of the token.

- Finality+fork-choice rules: Protocols like Ethereum’s combine fork-choice (LMD-GHOST) and a finality gadget (Casper FFG) to reduce fork windows and make reorgs costly. 
eth2book.info

Economic penalties

- Slashing destroys stake if validators sign conflicting checkpoints or break defined rules.

- Opportunity cost: stake used for attack cannot earn honest rewards and may fall in fiat value if trust collapses.

Real-world examples 
- Ethereum (post-Merge)
- Cardano
- Solana

Advantages

- Energy efficiency — vastly lower electricity use compared with PoW because consensus work is economic, not computational. (Estimates vary but PoS networks often claim orders-of-magnitude lower consumption.) 


- Lower operational cost — validators only need reliable nodes, not power-hungry ASICs.

- Faster finality — many PoS designs finalize blocks faster, reducing confirmation times.

Disadvantages

- Economic centralization risk — large holders stake more and may gain outsized influence; staking services and pools can centralize control.

- Nothing-at-stake & long-range attacks (theoretical) — early PoS designs faced “nothing-at-stake” concerns where validators could sign multiple forks at low cost; modern designs mitigate this with slashing, unbonding windows, and finality gadgets.

- Complexity — PoS protocols (randomness, slashing conditions, finality mechanisms) tend to be more complex to reason about and implement correctly.
### Comparative Analysis
[Your comparison table and analysis]

### Practical Implications for Creatives
 - Security Model: PoW has computational security, attacker needs >50% hashpower to dominate. Security tied to physical resources (hardware+energy) while 
PoS has economic security, attacker needs large stake; attack risks losing stake (slashing) and value collapse.

- Energy & environmental impact: PoW is energy-intensive and environmental footprint depends on energy mix and mining efficiency. while
PoS orders-of-magnitude lower electricity use (no continuous hash racing). Use fewer resources overall

- Transaction speed & throughput : Base PoW chains (Bitcoin) have lower throughput and higher latencies; scaling often via layer-2.

PoS chains frequently enable faster finality and higher block rates; many newer PoS chains optimize throughput on the base layer.

- Decentralization

PoW: decentralization depends on hardware distribution & pool dynamics; ASICs and cheap energy can centralize mining.

PoS: decentralization depends on stake distribution; exchanges and large holders can centralize staking. Both models face centralization pressures, but the vectors differ.

## Part 2: Gas, Blocks & Confirmations

### Gas Economics
- What is gas?

Gas is a unit that measures the work required to execute operations on a blockchain virtual machine (e.g., the Ethereum EVM). Think of gas as the fuel metered per computational step, storage read/write, or cryptographic operation. You pay for the gas in the chain’s native token (ETH on Ethereum) so validators/validators are compensated for processing your transaction. 


- Why gas?
The metaphor comes from real-world fuel: different operations consume different amounts of fuel (gas). It communicates that computation (not just bytes transferred) is being paid for.

- How gas pricing works

Gas price is how much ETH you pay per unit of gas. It’s typically expressed in Gwei (1 Gwei = 10⁻⁹ ETH). Wallets show gas-price suggestions in Gwei

- How gas price is determined

Market-driven: users compete for limited block-space. Higher offered tip means higher chance block builder picks your transaction. Base fee adjusts per-block based on demand. Tools (gas oracles) recommend price levels by looking at mempool and recent blocks. 


- Gas limit vs gas price

Gas limit = maximum gas units you allow the transaction to consume (a safety cap).

Gas price = how much you actually pay per unit.
Total paid = gasUsed × gasPrice

- Gas optimization strategies

When prices are lowest

Off-peak network usage — early mornings / weekends by global demand patterns — but times vary by chain and user base. Use gas trackers to see cheap windows. 

- How to reduce gas costs

- Use optimized smart-contract code (fewer storage writes, pack variables, minimize loops).

- Batch operations - Combine many operations into one transaction (e.g., a single contract call that executes multiple transfers).

- Use Layer 2s or alternative chains with lower base fees. 



### Blocks Structure
What is a block?

A block is a container or record that batches many transactions together and links them to the chain. Each block has header metadata, a list of transactions, and summary hashes that cryptographically represent the transactions. Nodes validate blocks and append them to the chain in order

- What information a block contains

Header: timestamp, previous block hash, nonce (PoW) or other consensus-specific fields, Merkle root of transactions, block number, difficulty/target (PoW) or state root, etc.

Body: ordered list of transactions and receipts.

Merkle root: compact fingerprint for the whole transaction set enabling efficient proofs.

- How blocks are linked

Each block stores the previous block’s hash in its header. Because the header is hashed, linking makes the chain tamper-evident: changing an old block would require redoing all later blocks’ proofs (PoW) or violating finality rules (PoS).

- How many transactions fit in a block?

Not a fixed number — depends on block gas limit (Ethereum) or block size (Bitcoin) and the size/gas cost of each transaction. Example: Ethereum blocks have a gas limit per block (a cap on total gas used by transactions inside it); if many complex txs are included the block holds fewer transactions

- What is block time?

The average time between new blocks being produced (e.g., Bitcoin ~10 minutes, Ethereum ~12–15 seconds, Solana ~400ms - few 100s ms depending on network). Block time depends on protocol design and consensus.

### Confirmations

-What are confirmations?

A confirmation is a count of how many blocks have been added on top of the block that contains your transaction. If your tx is in block N, and the chain tip is at N+3, your transaction has 3 confirmations. Each new block makes earlier blocks more difficult to revert.

-Why confirmations matter

They measure the probability that a transaction will not be reversed by a reorg (a competing longer chain replacing blocks). More confirmations → exponentially lower probability of successful rollback (in PoW) or stronger finality (in PoS where checkpoints/finality exist).

- How many confirmations are typical?

Bitcoin: 1–3 confirmations for small payments, 6 confirmations often considered “safe” for large transfers.

Ethereum: Because blocks are faster, exchanges often require 12–64 confirmations depending on value and policy (but with PoS finality, once a block is finalized via the finality gadget, it’s stronger). 

Why exchanges require more confirmations

To reduce the risk of double-spend and reorg-based loss. Exchanges are custodians — they set conservative confirmation thresholds based on chain characteristics, tx value, and historical reorg risk.

---

## Part 3: Wallet Security & Types

### Custodial vs Non-Custodial Wallets
What Are Custodial Wallets?

A custodial wallet is a wallet where a third party holds your private keys for you.
They act like a bank — you have an account, but they control the vault.

### Hot vs Cold Wallets
[Your research and comparison]

### Security Best Practices
[Your security checklist and recommendations]

---

## Part 4: Testnets & Blockchain Explorers

### Testnets
[Your research and hands-on experience]

### Blockchain Explorers
[Your research and practical examples]

---

## Part 5: MEV (Maximal Extractable Value)

### Understanding MEV
[Your research]

### Impact on Users
[Your analysis]

### MEV Solutions
[Your research]

---

## Part 6: Transaction Analysis

📖 See your separate transaction analysis document: `your-name-transaction-analysis.md`

---

## Comparison Tables

### PoW vs PoS Comparison

| Feature | Proof of Work | Proof of Stake |
|---------|---------------|----------------|
| Security Model | | |
| Energy Consumption | | |
| Transaction Speed | | |
| Decentralization | | |
| Entry Barrier | | |
| Cost Structure | | |
| Scalability | | |

### Custodial vs Non-Custodial Wallets

| Feature | Custodial | Non-Custodial |
|---------|-----------|---------------|
| Security | | |
| Convenience | | |
| Control | | |
| Recovery | | |
| Use Cases | | |

### Hot vs Cold Wallets

| Feature | Hot Wallet | Cold Wallet |
|---------|------------|-------------|
| Security Level | | |
| Convenience | | |
| Cost | | |
| Best For | | |

---

## Key Takeaways
[Write 5-7 key insights you learned]

---

## All Sources and References
1. [Source 1]
2. [Source 2]
3. [Source 3]
[List all sources used in your research]

---

**Twitter Thread:** [Add your tweet link here]