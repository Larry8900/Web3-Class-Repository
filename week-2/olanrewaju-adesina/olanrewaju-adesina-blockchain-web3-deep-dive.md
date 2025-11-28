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
You sign up with an account (email/phone).
The provider stores your private keys on their servers.
They manage backups, security, and recovery.
You send/receive crypto through their interface without touching keys.

- Advantages

Easy to use (no seed phrase needed).
Recovery is possible if you lose your login.
Great for beginners.
Fast support and integrated services (buy, sell, swap, earn).
Lower risk of losing funds due to user errors.

- Risks
Not your keys, not your crypto.
If the company is hacked, bankrupt, or freezes your account, you lose access.
Subject to KYC, regulations, and withdrawal delays.
You rely on their security practices.

Examples of Custodial Wallet Providers : Binance Wallet, Coinbase Wallet, KuCoin, Bybit, etc

- What Are Non-Custodial Wallets?

Is a wallet where you control your private keys, meaning you have full responsibility for your crypto.
A wallet generates a seed phrase.
No third party can move your assets.
Everything is signed locally on your device.

- Advantages
Full control of your assets.
No account freezes or KYC.
Essential for Web3 (NFTs, DeFi, DAOs).
More privacy.

- Risks
If you lose your seed phrase, your funds are gone forever.
You are responsible for securing your device.
High risk of phishing, malware, and human mistakes.
No customer support can recover lost funds.

Examples of Non-Custodial Wallet Providers : MetaMask, Trust Wallet,Phantom, Ledger, etc

### Hot vs Cold Wallets

Hot Wallets are Wallets connected to the internet (web, mobile, desktop).
The private keys are stored on your internet-connected device with easy interaction with dApps, NFTs, and DeFi.

Cold Wallets are wallets stored offline, with keys never touching the internet. 
Device generates private keys offline and when signing transactions, the signature is done inside the device, The private key never leaves the device.

### Security Best Practices
- Seed Phrase Security 

Write it on paper or metal.
Store offline in two separate locations.
Never type it on websites.
Never store it in email, photos, or cloud.

- How to Protect Yourself

Always double-check URLs.
Never share your seed phrase.
Use hardware wallets.
Enable 2FA for custodial accounts.
Use antivirus and VPN.
Keep wallets updated.


## Part 4: Testnets & Blockchain Explorers

### Testnets

- What Are Testnets?

Testnets are practice versions of blockchains where everything is free and nothing has real value. Projects use testnets to simulate new features before deploying to mainnet.

- Why Testnets Exist

Developers need a safe environment to test smart contracts, apps, and upgrades.

Beginners need a place to practice sending transactions without losing money.

- How Testnets Differ From Mainnet

1. Token value	 is Free and worthless on Testnets but has	Real monetary value in mainet
2. Testnets has zero risk while mainet has High
3. Testnets Purpose	is basically for testing and learning but mainnet is for real transactions
4. Network security on testnet is Lower	but much higher on mainnet 
5. Cost of transactions	is basically free/near-zero	on testnet but you pay Real gas fees on mainnet

Popular Testnets 

1. Sepolia Testnet (Ethereum)
Current recommended Ethereum testnet.
Uses ETH (test ETH) for gas.
Stable, actively maintained.
Works with most DeFi, NFT, and dApp testing tools.
Replaced older testnets (Ropsten, Rinkeby, Kovan, Goerli).

2. Mumbai Testnet (Polygon)
Polygon’s main testnet.
Uses test MATIC as gas.
Very fast and cheap.
Often used to test NFT mints and gaming projects.

- Other Major Testnets

Arbitrum Sepolia – Layer 2 testing.
Base Sepolia – Coinbase L2 testnet.
BNB Chain Testnet – For BEP20 projects.
Solana Devnet/Testnet – High-throughput app testing.

How to Use Testnets
1. Connect to a Testnet in MetaMask
Open MetaMask
Click Network Dropdown
Toggle “Show Test Networks” in Settings
Select: Sepolia (ETH)
        Mumbai (Polygon)
        Or add custom RPC manually

- How to Get Test Tokens

Go to a faucet. Examples:
Sepolia Faucet: Google “Ethereum Sepolia Faucet”
Mumbai Faucet: https://mumbaifaucet.com
Most faucets ask you to: Paste your wallet address
Solve CAPTCHA
Claim free test tokens

- What You Can Practice on Testnets

1. Sending and receiving transactions
2. Minting NFTs
3. Interacting with DeFi apps
4. Deploying your own smart contracts
5. Testing dApps before using real money
6. Practicing wallet navigation without risk

- Limitations of Testnets

1. Tokens have no real value
2. Sometimes slow or unavailable
3. Some apps are not deployed on testnets
4. Security is weaker than mainnet
5. Faucets may be limited or spam-protected

### Blockchain Explorers

Blockchain explorers are search engines for blockchains.
Just like Google lets you search the web, explorers let you search the blockchain. 

- Why Are Blockchain Explorers Important?

They help you:
1. Check if a transaction succeeded
2. Verify your NFT ownership
3. Investigate wallet activity
4. Track smart contract interactions
5. See gas prices and network status
6. Debug failed transactions

- What You Can Do With Them
1. Search wallet addresses
2. Search transaction hashes
3. View tokens and NFTs
4. Read contract code
5. Check node data, blocks, fees, analytics
6. Check token approvals and revoke permissions

- Etherscan Deep Dive 

How to Search for Transactions

Copy transaction hash → paste in Etherscan search bar
View: Status (Success/Failed/Pending)
Gas used
Sender & receiver
Timestamp
Value sent
Wallet interactions

-How to Read Transaction Details

Key fields:
Status – success or failure
From/To – addresses involved
Nonce – transaction count
Gas Used vs Gas Limit
Fee Paid
Input Data (function call)
Block Number
Timestamp

- How to Explore Wallet Addresses

Paste a wallet into Etherscan:
See all incoming & outgoing transactions
Token balances
NFT holdings
Contract interactions
Transaction history of years

- Other Blockchain Explorers
1. Polygonscan (Polygon)
Similar to Etherscan
Used for MATIC transactions
Great for NFT gaming activity

2. Solscan (Solana)
Tracks high-speed Solana transactions
Shows token accounts, NFTs, and stake accounts
Useful for debugging Solana programs

3. BscScan (BNB Chain)
For BEP-20 tokens and DeFi apps
Same interface as Etherscan

4. Arbiscan (Arbitrum)
Layer 2 ETH explorer
Good for cheap DeFi & swaps

- Practical Use Cases of Blockchain Explorers

1. Verify NFT Ownership
Search your wallet
Go to ERC-721 / NFT tab
View the NFT contract, ID, metadata

2. Check Transaction Status
Pending
Success
Failed
Dropped
Replaced (speed-up / cancel)

3. Investigate a Wallet
Track whale wallets
Check if a project is rugging
Watch suspicious movement
Analyze buying/selling behavior

4. Verify Smart Contract Code
Ensure code is verified
Read source code
See if contract is upgradeable
Check if it contains mint functions, freeze functions, pausable functions

5. Track Gas Prices
Use Gas Tracker to optimize timing
Know when network is congested
Save money on mints or swaps

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