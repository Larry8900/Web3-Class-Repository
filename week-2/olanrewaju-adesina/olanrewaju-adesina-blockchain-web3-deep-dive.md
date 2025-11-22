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
[Your research]

### Blocks Structure
[Your research]

### Confirmations
[Your research]

---

## Part 3: Wallet Security & Types

### Custodial vs Non-Custodial Wallets
[Your research and comparison]

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