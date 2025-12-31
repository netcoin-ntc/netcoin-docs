# Netcoin Complete Testing Guide: DevNet, QANet & TestNet

This comprehensive guide walks you through deploying and using Netcoin's three testing networks - DevNet, QANet, and TestNet - for complete end-to-end testing of all Netcoin features with different parameters for various testing scenarios.

## Netcoin Testing Networks Overview

Netcoin provides three distinct testing networks, each optimized for different testing scenarios. All networks are **production-ready** and include the complete Netcoin feature set with advanced privacy cryptography.

### Network Comparison Table

| Feature | **DevNet** | **QANet** | **TestNet** | **MainNet** |
|---------|------------|-----------|-------------|-------------|
| **Purpose** | Development & Feature Testing | Formal QA & Benchmarking | Community Testing | Production |
| **Block Time** | 30 seconds | 10 minutes | 2 minutes | 10 minutes |
| **Difficulty** | 1 (very easy) | 10,000 (medium) | 50,000 (challenging) | Variable |
| **Genesis Allocation** | 0 NTC | 1,000 NTC | 10,000 NTC | 0 NTC |
| **Mining Reward** | 100 NTC/block | 100 NTC/block | 100 NTC/block | Variable |
| **Network ID** | `"devnet"` | `"qanet"` | `"testnet"` | `"mainnet"` |
| **Fast Sync** | ✅ Enabled | ✅ Enabled | ✅ Enabled | ❌ Disabled |
| **Debug Mode** | ✅ Enabled | ❌ Disabled | ❌ Disabled | ❌ Disabled |
| **Public Access** | Internal only | Internal only | Public | Public |
| **Best For** | Rapid iteration | Performance testing | Community validation | Real transactions |

### DevNet: Development Network
**Perfect for rapid development and feature testing**

```bash
# Test all DevNet features automatically
cd netcoin-internal/scripts
./demo-all-features.sh devnet
```

**Characteristics:**
- ⚡ **30-second blocks** - Fast iteration and testing
- 🎯 **Difficulty 1** - Instant mining for development
- 🛠️ **Debug enabled** - Full logging and error details
- 🔄 **Resettable** - Clean state for testing scenarios
- 💰 **No premine** - Earn NTC through mining

### QANet: Quality Assurance Network
**Optimized for formal testing and benchmarking**

```bash
# Test all QANet features automatically
cd netcoin-internal/scripts
./demo-all-features.sh qanet
```

**Characteristics:**
- 📊 **10-minute blocks** - Bitcoin-like parameters
- 🎯 **Difficulty 10k** - Realistic mining challenge
- 📈 **Performance monitoring** - TPS and latency metrics
- 🔬 **Regression testing** - Automated QA pipelines
- 🎭 **Production simulation** - Real-world testing conditions

### TestNet: Community Testing Network
**Designed for community validation and feedback**

```bash
# Test all TestNet features automatically
cd netcoin-internal/scripts
./demo-all-features.sh testnet
```

**Characteristics:**
- 🌐 **2-minute blocks** - Balanced for community testing
- 🎯 **Difficulty 50k** - Challenging but achievable
- 👥 **Community faucet** - Free NTC distribution
- 📊 **Global nodes** - Worldwide testing infrastructure
- 🐛 **Bug bounty ready** - Issue tracking and reporting

### Network Isolation Verification

All networks are **completely isolated** - test on one network doesn't affect others:

```bash
# Test network isolation
cd netcoin-internal/scripts
./test-all-networks.sh
```

**What gets tested:**
- ✅ DevNet wallets don't exist on TestNet
- ✅ QANet blocks don't appear on DevNet
- ✅ TestNet transactions don't affect QANet
- ✅ Complete blockchain separation
- ✅ Independent genesis blocks
- ✅ Isolated mining rewards

### Automated Feature Testing

Netcoin provides comprehensive automated testing for all networks:

#### **Complete Feature Demo (Recommended)**
```bash
# Test ALL features on any network
./demo-all-features.sh [devnet|qanet|testnet]

# Example outputs:
# DevNet: 60+ blocks mined in 30 seconds
# QANet: Realistic Bitcoin-like mining
# TestNet: Community-scale testing
```

#### **Network Isolation Testing**
```bash
# Verify all networks are properly separated
./test-all-networks.sh
```

#### **Manual Testing Options**
```bash
# Build and initialize any network
cd netcoin-core
./target/release/netcoin-devnet init  # Uses devnet by default

# Switch to different network
cp qanet-config.json devnet-config.json
./target/release/netcoin-devnet init

# Mine on any network
cd ../netcoin-miner
./target/release/netcoin-miner mine --wallet @your-address

# Use CLI on any network
cd ../netcoin-core
./target/release/netcoin-cli --network qanet wallet balance @address
```

### Features Available on All Networks

All three testing networks include the **complete Netcoin feature set**:

#### ✅ Core Cryptocurrency Features
- **Proof-of-Work Mining** - CPU-focused with adjustable difficulty
- **UTXO Blockchain** - Unspent transaction output model
- **Wallet Management** - 24-word BIP39 seed phrases
- **Transaction Processing** - Full validation and confirmation

#### ✅ Advanced Privacy Features
- **MLSAG Ring Signatures** - 16-member anonymity sets
- **Bulletproofs** - Zero-knowledge range proofs
- **Confidential Transactions** - Amount hiding with Pedersen commitments
- **Stealth Addresses** - One-time recipient addresses
- **ElGamal Encryption** - IND-CCA2 secure memo encryption

#### ✅ User Experience Features
- **@Alias System** - Human-readable @usernames (0.1 NTC fee)
- **Command-Line Interface** - Full wallet and transaction management
- **RPC Server** - Mining coordination and block submission
- **Network Statistics** - Real-time blockchain metrics

#### ✅ Development Features
- **Multi-Node Support** - Consensus testing and validation
- **Automated Testing** - Comprehensive feature verification
- **Debug Logging** - Detailed operation visibility
- **Clean State Management** - Reset and cleanup capabilities

### Getting Started with Testing

#### **Quick Start (DevNet Recommended)**
```bash
# 1. Build Netcoin
cd netcoin-ntc
cd netcoin-core && cargo build --release
cd ../netcoin-miner && cargo build --release

# 2. Run complete feature demonstration
cd ../netcoin-internal/scripts
./demo-all-features.sh devnet
```

#### **Expected DevNet Results:**
```
✅ DevNet initialized
✅ RPC server running
✅ 2 wallets created with 24-word seeds
✅ Mining: 60+ blocks in 30 seconds
✅ Balance persistence working
✅ Confidential transactions sent
✅ @Alias registration successful
✅ Stealth addresses generated
✅ All privacy features verified
```

#### **Testing Different Scenarios:**

**For Development Speed:**
```bash
./demo-all-features.sh devnet   # 30s blocks, instant mining
```

**For Realistic Testing:**
```bash
./demo-all-features.sh qanet    # 10min blocks, Bitcoin-like
```

**For Community Simulation:**
```bash
./demo-all-features.sh testnet  # 2min blocks, challenging mining
```

### Advanced Testing Scenarios

#### **Performance Benchmarking**
```bash
# Test mining performance across networks
./demo-all-features.sh devnet   # Measure hashrates and block times
./demo-all-features.sh qanet    # Test realistic mining conditions
```

#### **Privacy Feature Validation**
```bash
# All networks include identical privacy features
./demo-all-features.sh devnet   # Fast privacy testing
./demo-all-features.sh testnet  # Community-scale privacy
```

#### **Network Consensus Testing**
```bash
# Test multi-node consensus (all networks support this)
./test-all-networks.sh          # Verify network isolation
```

### Troubleshooting Network Testing

#### **Common Issues:**

**"Command not found"**
```bash
# Ensure binaries are built
cd netcoin-core && cargo build --release
cd ../netcoin-miner && cargo build --release
```

**"Network not initialized"**
```bash
# Initialize the specific network
cd netcoin-core
cp [network]-config.json devnet-config.json
./target/release/netcoin-devnet init
```

**"Mining takes too long"**
```bash
# Use DevNet for fast mining
./demo-all-features.sh devnet  # 30s blocks, difficulty 1
```

**"Balance shows zero"**
```bash
# Mining rewards need time to process
# DevNet: Check after 30 seconds of mining
# QANet/TestNet: May take several minutes
```

### Network Selection Guide

| **When to Use** | **Recommended Network** | **Why** |
|-----------------|-------------------------|---------|
| **First-time testing** | DevNet | Fast results, easy mining |
| **Realistic performance** | QANet | Bitcoin-like parameters |
| **Community simulation** | TestNet | Global testing scale |
| **Privacy feature testing** | Any | All networks identical |
| **Mining algorithm testing** | DevNet | Fast iteration |
| **UI/UX development** | DevNet | Quick feedback loops |
| **Security testing** | QANet/TestNet | Production-like conditions |
| **Performance benchmarking** | QANet | Realistic load testing |

### Next Steps After Testing

1. **Run Automated Tests** - Verify all features work
2. **Explore Advanced Features** - Try different transaction types
3. **Multi-Node Testing** - Deploy consensus networks
4. **Performance Analysis** - Benchmark mining and transactions
5. **Integration Testing** - Connect external applications

---

## Prerequisites
- [DevNet Architecture](#devnet-architecture)
- [Step 1: DevNet Deployment](#step-1-devnet-deployment)
- [Step 2: Wallet Creation](#step-2-wallet-creation)
- [Step 3: Understanding Privacy Features](#step-3-understanding-privacy-features)
- [Step 4: @Alias System](#step-4-alias-system)
- [Step 5: Privacy Transactions](#step-5-privacy-transactions)
- [Step 6: Multi-Node Deployment](#step-6-multi-node-deployment)
- [Step 7: Advanced Operations](#step-7-advanced-operations)
- [Step 8: Troubleshooting](#step-8-troubleshooting)
- [DevNet vs MainNet Differences](#devnet-vs-mainnet-differences)

## Prerequisites

### System Requirements
- **OS**: Linux, macOS, or Windows (Linux recommended)
- **RAM**: 4GB minimum (8GB recommended)
- **Storage**: 10GB free space
- **Network**: Stable internet connection

### Software Dependencies
- **Rust**: Latest stable version (1.70+)
- **Git**: Version control system
- **Terminal/Command Prompt**: For running commands

### Installation
```bash
# Clone the repository
git clone https://github.com/netcoin-ntc/netcoin-ntc.git
cd netcoin-ntc

# Install Rust (if not already installed)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env

# Build netcoin-core (node + wallet)
cd netcoin-core
cargo build --release

# Build netcoin-miner (mining software)
cd ../netcoin-miner
cargo build --release

# Return to netcoin-core for usage
cd ../netcoin-core
```

## DevNet Architecture

### DevNet Parameters
| Parameter | DevNet Value | MainNet Value | Purpose |
|-----------|-------------|---------------|---------|
| Block Time | 30 seconds | 10 minutes | Rapid testing |
| Mining Difficulty | 1 | Variable | Easy mining |
| Genesis Allocation | None | 0 NTC | No pre-mined funds |
| Network ID | "devnet" | "mainnet" | Network isolation |
| Fast Sync | Enabled | Disabled | Quick startup |

### DevNet Components
- **netcoin-devnet**: DevNet management CLI
- **netcoin-cli**: Wallet and transaction CLI
- **Genesis Block**: Pre-allocated test NTC
- **Configuration**: devnet-config.json
- **Data Directory**: ./devnet-data/

## Step 1: DevNet Deployment

### Initialize DevNet
```bash
# Navigate to netcoin-core directory
cd netcoin-ntc/netcoin-core

# Initialize DevNet (creates config and genesis block)
./target/release/netcoin-devnet init
```

**Expected Output:**
```
🏗️  Initializing Netcoin DevNet...
🚀 Deploying single DevNet node...
🌟 Creating DevNet genesis block...
✅ Genesis block created: ./devnet-data/genesis.dat
✅ DevNet node deployed successfully!
   📁 Data directory: ./devnet-data
   🌐 Network: devnet
   🧑‍💻 Ready for mining and transactions!

🌐 Netcoin DevNet Configuration
   📍 Network ID: devnet
   ⏱️  Block Time: 30 seconds
   ⚡ Mining Difficulty: 1
   💰 Genesis Allocation: None
   🚀 Fast Sync: Enabled
   🐛 Debug Mode: Enabled
   📁 Data Directory: ./devnet-data

🎯 DevNet initialized! Next steps:
   1. Start mining: netcoin-node --devnet
   2. Create wallet: netcoin-cli wallet create
   3. Send transactions: netcoin-cli tx send <from> <to> <amount>
   4. Test @aliases: netcoin-cli alias register <name> --wallet <addr>
```

### Verify DevNet Status
```bash
# Check DevNet configuration and status
./target/release/netcoin-devnet status
```

**Expected Output:**
```
🌐 Netcoin DevNet Configuration
   📍 Network ID: devnet
   ⏱️  Block Time: 30 seconds
   ⚡ Mining Difficulty: 1
   💰 Genesis Allocation: None
   🚀 Fast Sync: Enabled
   🐛 Debug Mode: Enabled
   📁 Data Directory: ./devnet-data

✅ Genesis block: Present
✅ Data directory: Present
📦 Blocks mined: 0 (ready for mining)
```

### Files Created
```
devnet-config.json      # DevNet configuration
./devnet-data/          # DevNet data directory
  ├── genesis.dat       # Genesis block
  ├── blockchain.dat    # Real blockchain state (after mining)
  └── ...               # Additional blockchain data
```

## Step 2: Wallet Creation

### Create Your First Wallet
```bash
# Create a new wallet
./target/release/netcoin-cli wallet create
```

**Expected Output:**
```
🔐 Creating new Netcoin wallet...
✅ Wallet created successfully!
📍 Address: @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d
🔐 Seed Phrase (24 words - SAVE THIS SECURELY):
   abandon abandon abandon abandon abandon abandon abandon abandon abandon abandon abandon about

⚠️  IMPORTANT SECURITY REMINDERS:
   • Write down these 24 words in order
   • Store in a secure, offline location
   • Never share with anyone
   • This is your only way to recover funds
   • Consider adding a passphrase for extra security
💾 Wallet saved to: /home/user/.netcoin
```

### Understanding Your Wallet
- **Address**: Your public wallet address (starts with @ for stealth addresses)
- **Seed Phrase**: 24-word BIP39 mnemonic for wallet recovery
- **Stealth Address**: One-time addresses for maximum privacy
- **View Key**: Allows seeing incoming transactions without spending ability

### Check Wallet Balance
```bash
# Check balance (initially zero on DevNet)
./target/release/netcoin-cli wallet balance @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d
```

**Expected Output:**
```
💰 Checking balance for @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d...
❌ Wallet @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d not found or has zero balance
💡 If this is a new wallet, it needs to receive funds first
💡 Try: netcoin-cli tx receive @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d
```

## Step 3: Understanding Privacy Features

### Netcoin's Privacy Stack

Netcoin implements the most advanced privacy features available:

#### 1. **Ring Signatures (MLSAG)**
- **Purpose**: Hide transaction sender among multiple decoys
- **Strength**: 16-member ring signatures
- **Benefit**: Sender anonymity against blockchain analysis

#### 2. **Confidential Transactions**
- **Purpose**: Hide transaction amounts
- **Technology**: Pedersen Commitments + Bulletproofs
- **Benefit**: Amount privacy while maintaining verification

#### 3. **Stealth Addresses**
- **Purpose**: Hide transaction recipients
- **Technology**: One-time addresses derived via ECDH
- **Benefit**: Perfect forward secrecy for recipients

#### 4. **@Alias System**
- **Purpose**: Human-readable addresses
- **Technology**: NTC-powered registration with stealth address mapping
- **Benefit**: Usability without compromising privacy

#### 5. **ElGamal Encryption**
- **Purpose**: Encrypt transaction memos
- **Technology**: IND-CCA2 secure encryption
- **Benefit**: Private transaction metadata

### Privacy Demonstration
Every Netcoin transaction shows these features in action:

```
🔐 Privacy Features Applied:
   ✅ MLSAG Ring Signature (16 decoy outputs)
   ✅ Bulletproofs Range Proof (amount validity)
   ✅ Pedersen Commitment (amount hiding)
   ✅ ElGamal Encryption (memo protection)
   ✅ Stealth Address (recipient privacy)
```

## Step 3.5: Mining and Earning NTC

### Start DevNet Mining
Netcoin uses a dedicated mining client (`netcoin-miner`) for better performance and security. Mining rewards go directly to your wallet address.

```bash
# Terminal 1: Start DevNet node
./target/release/netcoin-devnet init

# Terminal 2: Start mining to your wallet
../netcoin-miner/target/release/netcoin-miner mine --wallet @your-wallet-address
```

**Expected Output:**
```
⛏️  Netcoin Miner v0.1.0
   🎯 Wallet: @your-wallet-address
   🌐 Node: http://127.0.0.1:8332
   🧵 Auto-detected 8 CPU threads
   🧵 Using 8 threads
   🎯 Mining mode: Solo mining
   💰 Rewards will go to: @your-wallet-address

🚀 Starting Netcoin mining...
   Press Ctrl+C to stop mining

✅ Block 1 mined in 0.02s! 🎉 (Hashrate: 50,000 H/s)
   💰 Mining reward sent to: @your-wallet-address
✅ Block 2 mined in 0.01s! 🎉 (Hashrate: 100,000 H/s)
   💰 Mining reward sent to: @your-wallet-address
...
```

### Mining Parameters
- **Algorithm**: CPU mining (RandomX-ready)
- **Difficulty**: Very low for DevNet testing
- **Block Reward**: 100 NTC per block
- **Block Time**: ~1-5 seconds (DevNet accelerated)
- **Miner Address**: Your specified wallet receives rewards

### Check Your Mining Rewards
```bash
# Check your wallet balance to see mining rewards
./target/release/netcoin-cli wallet balance @your-wallet-address
```

**Expected Output:**
```
💰 Checking balance for @your-wallet-address...
🔍 Checking for DevNet config at: "devnet-config.json"
📁 Current directory: "/path/to/netcoin-core"
📄 Config exists: true
🌐 DevNet detected - querying actual blockchain...
✅ DevNet Balance: 200.00 NTC (from 2 mined blocks)
📊 Satoshis: 200000000000
🏆 Mining Rewards: 2 blocks × 100 NTC
```

### Mining Options
```bash
# Mine with specific thread count
../netcoin-miner/target/release/netcoin-miner mine --wallet @your-wallet --threads 4

# Mine to different wallet
../netcoin-miner/target/release/netcoin-miner mine --wallet @another-wallet

# Pool mining (future feature)
../netcoin-miner/target/release/netcoin-miner mine --pool pool.example.com:3333 --wallet @your-wallet
```

### Understanding Mining Rewards
- **Your Wallet**: Mining rewards go directly to your specified address
- **Real NTC**: Creates actual spendable NTC on the blockchain
- **DevNet Testing**: Perfect for testing privacy features with real funds
- **No Genesis Dependency**: Unlike old system, you control your mining rewards

### Mining Performance
- **CPU Mining**: Uses all available CPU cores by default
- **Hashrate**: Scales with CPU performance and core count
- **Efficiency**: Optimized for fast DevNet block times
- **Low Resource**: Minimal memory and disk usage

### Stop Mining
```bash
# Press Ctrl+C in the mining terminal
# Mining stops gracefully and shows final statistics
```

### Mining Benefits for Testing
- **Real Blockchain**: Creates actual blocks and transactions
- **Economic Testing**: Validates mining rewards and distribution
- **Balance Testing**: Provides NTC for wallet operations
- **Privacy Testing**: Enables full end-to-end privacy feature testing
- **Performance Benchmarking**: Tests mining speed and efficiency

## Step 4: @Alias System

### Check Alias Availability
```bash
# Check if an alias is available
./target/release/netcoin-cli alias check mywallet
```

**Expected Output:**
```
🔍 Checking availability of alias @mywallet...
✅ Alias @mywallet is valid and available!

📋 Alias Requirements Met:
   • Length: 8 characters (1-32 allowed)
   • Format: Lowercase alphanumeric + underscores/dashes
   • Reserved: Not a system-reserved name
   • Unique: Not currently registered

💰 Registration Cost: 0.1 NTC
🔐 Privacy Benefit: Maps to your stealth address
```

### Alias Requirements
- **Length**: 1-32 characters
- **Format**: Lowercase letters, numbers, underscores (_), dashes (-)
- **Rules**: Must start and end with alphanumeric character
- **Reserved**: Words like "admin", "root", "system", "netcoin" are reserved
- **Cost**: 0.1 NTC registration fee

### Register an Alias
```bash
# Register an alias for your wallet
./target/release/netcoin-cli alias register mywallet --wallet @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d
```

**Expected Output:**
```
Registering alias @mywallet for wallet @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d...
✅ Alias @mywallet registered successfully!
💰 Registration fee: 0.1 NTC
👤 Owned by: @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d
🔐 Privacy: Stealth address components stored
📅 Expires: Never (no expiration for demo)
```

### Lookup an Alias
```bash
# Resolve an alias to its stealth address components
./target/release/netcoin-cli alias lookup mywallet
```

**Expected Output:**
```
🔎 Looking up alias @mywallet...
✅ Alias @mywallet found!
🔑 Scan Key: 56c5980d19fb756c5478efe31c7214f13cc7d22bf1e825d7d3471a924106850f
🔑 Spend Key: 76109738129006bb627ed32ee777ee9cf418ccf65bdcc08b509bdb0c63da1315
👤 Owner: @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d
💰 Registration Fee: 0.1 NTC
📅 Registered: 1766864083
📝 Description: Alias registered for wallet @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d

🔐 Privacy Note: This resolves to stealth address components
   for maximum recipient privacy.
```

### List Your Aliases
```bash
# List all aliases owned by a wallet
./target/release/netcoin-cli alias list @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d
```

**Expected Output:**
```
Listing aliases for wallet @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d...
✅ Found 1 aliases owned by @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d:

@mywallet
  💰 Fee: 0.1 NTC
  📅 Registered: 1766864083
  📝 Description: Alias registered for wallet @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d
```

## Step 5: Privacy Transactions

### Generate Receive Address
```bash
# Generate a one-time receive address
./target/release/netcoin-cli tx receive @mywallet
```

**Expected Output:**
```
📨 Generating new receive address...
✅ New receive address generated!
📍 One-time Address: @9a067391f411ab52d629d5f96acde2f37a910a4ca6811472137288130b72a609
🔑 Transaction Public Key: 70a2dc87b422be3a1839cb31cdb32c59f3d93d6b6b67dc185f7fb14c9dfa1028

🔐 Privacy Features:
   • One-time address (different for each payment)
   • Perfect forward secrecy
   • Unlinkable from your main wallet address
   • Only you can detect payments to this address

💡 Share this address with the sender for maximum privacy
⚠️  This address can only be used once for privacy
```

### Send Privacy Transaction
```bash
# Send NTC with privacy features and memo
./target/release/netcoin-cli tx send @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d @recipient 0.5 --memo "Lunch payment"
```

**Expected Output:**
```
💸 Sending 0.5 NTC from @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d to @recipient...
📝 Memo: Lunch payment
🔄 Processing transaction...
   📊 Amount: 0.5 NTC (500000000 netpennies)
   👤 From: @86867159e9a62b8eb9d333119c097d6677209f73486f576eddb3e620b153bb6d
   🎯 To: @recipient
   🔗 Transaction ID: tx_1b1f693e5258142cf981529e78281e32

🔐 Privacy Features Applied:
   ✅ MLSAG Ring Signature (16 decoy outputs)
   ✅ Bulletproofs Range Proof (amount validity)
   ✅ Pedersen Commitment (amount hiding)
   ✅ ElGamal Encryption (memo protection)
   ✅ Stealth Address (recipient privacy)

📡 Broadcasting transaction...
⏳ Waiting for confirmations...
✅ Transaction sent successfully!
🔗 TXID: tx_1b1f693e5258142cf981529e78281e32
📊 Fee: 0.001 NTC
⚡ Confirmations: 1/6 (estimated 2 minutes)

🔒 Transaction Privacy:
   • Amount hidden from blockchain observers
   • Sender identity protected by ring signatures
   • Recipient address unlinkable from main wallet
   • Memo encrypted with recipient's public key
   • Encrypted memo: 13 bytes
```

### Send to Alias
```bash
# Send NTC to an alias (resolves to stealth address)
./target/release/netcoin-cli tx send @mywallet @friend 1.0 --memo "Gift"
```

**Same privacy features apply, but with human-readable addressing.**

## Step 6: Multi-Node Deployment

### Deploy Multiple Nodes
```bash
# Deploy 3 additional DevNet nodes
./target/release/netcoin-devnet deploy 3
```

**Expected Output:**
```
🚀 Deploying 3 DevNet nodes...
✅ Node 1 deployed
✅ Node 2 deployed
✅ Node 3 deployed
🎉 All 3 DevNet nodes deployed!
```

### Check DevNet Configuration
```bash
# View DevNet configuration
./target/release/netcoin-devnet config
```

**Expected Output:**
```
🌐 Netcoin DevNet Configuration
   📍 Network ID: devnet
   ⏱️  Block Time: 30 seconds
   ⚡ Mining Difficulty: 1
   💰 Genesis Allocation: None
   🚀 Fast Sync: Enabled
   🐛 Debug Mode: Enabled
   📁 Data Directory: ./devnet-data
```

## Step 7: Advanced Operations

### Network Status
```bash
# Check P2P network status
./target/release/netcoin-cli info network-status
```

**Expected Output:**
```
🌐 Network Status:
  📍 Node ID: node_50498765232a334122678b76306d5391
  🔌 Port: 8333
  👥 Peers Connected: 0
  📦 Best Block Height: 0
  💸 Transaction Pool: 0 transactions
  ⏱️  Uptime: 0 seconds

🔗 P2P Network Features:
   • Message serialization with bincode
   • Transaction broadcasting
   • Block announcement propagation
   • Alias registry synchronization

📱 Light Client Ready:
   • SPV verification support
   • Merkle proof validation
   • Mobile wallet compatibility
   • Reduced bandwidth requirements
```

### Privacy Statistics
```bash
# View privacy features overview
./target/release/netcoin-cli info privacy
```

**Expected Output:**
```
Privacy Statistics:
  Ring Signature Size: 16 members
  Confidential Transactions: Enabled
  Stealth Addresses: Enabled
  ElGamal Encryption: IND-CCA2
  @Alias System: Enabled
```

## Step 8: Troubleshooting

### Common Issues

#### DevNet Not Initialized
**Error:** `DevNet not initialized. Run: netcoin-devnet init`
**Solution:**
```bash
./target/release/netcoin-devnet init
```

#### Wallet Balance Zero
**Issue:** New wallets start with zero balance
**Solution:** Need to receive NTC from mining or other wallets

#### Alias Registration Fails
**Issue:** Insufficient balance or invalid alias format
**Solution:**
- Ensure wallet has at least 0.1 NTC
- Check alias format (lowercase, alphanumeric, 1-32 chars)

#### Transaction Broadcasting Fails
**Issue:** Network connectivity or invalid transaction
**Solution:**
- Check network status with `netcoin-cli info network-status`
- Verify recipient address/alias exists
- Ensure sufficient balance for amount + fee

### Reset DevNet
```bash
# Completely reset DevNet
./target/release/netcoin-devnet reset
```

### Clean Up DevNet
```bash
# Remove all DevNet data
./target/release/netcoin-devnet clean
```

## DevNet vs MainNet Differences

| Feature | DevNet | MainNet |
|---------|--------|---------|
| **Block Time** | 30 seconds | 10 minutes |
| **Mining Difficulty** | 1 (very easy) | Variable (~10^12) |
| **Genesis Allocation** | None | 0 NTC |
| **Network ID** | "devnet" | "mainnet" |
| **Fast Sync** | Enabled | Disabled |
| **Debug Logging** | Enabled | Disabled |
| **Reset Capability** | Yes | No |
| **Test Features** | Enabled | Disabled |

### Migration Path
1. **DevNet**: Feature development and testing
2. **QANet**: Formal QA and performance testing
3. **TestNet**: Community testing and feedback
4. **MainNet**: Production network with real economic value

---

## 🧪 Complete A to Z Testing Workflow

### Full DevNet Testing Sequence

Follow this complete workflow to test all Netcoin features end-to-end:

#### **Step 1: Initialize DevNet**
```bash
cd netcoin-ntc/netcoin-core
./target/release/netcoin-devnet init
```

#### **Step 2: Start Mining (Background)**
```bash
# Terminal 1: Start mining to generate NTC
./target/release/netcoin-devnet mine &
```

#### **Step 3: Create Wallets**
```bash
# Terminal 2: Create test wallets
./target/release/netcoin-cli wallet create  # Wallet A
./target/release/netcoin-cli wallet create  # Wallet B
```

#### **Step 4: Mine Some Blocks**
```bash
# Let mining run for 2-3 minutes to generate NTC
# Check: ./target/release/netcoin-devnet status
```

#### **Step 5: Register Aliases**
```bash
# Register human-readable aliases
./target/release/netcoin-cli alias register alice --wallet @<wallet-a-address>
./target/release/netcoin-cli alias register bob --wallet @<wallet-b-address>
```

#### **Step 6: Send Privacy Transactions**
```bash
# Send NTC between aliases with full privacy
./target/release/netcoin-cli tx send @alice @bob 0.5 --memo "Test transaction"
./target/release/netcoin-cli tx send @bob @alice 0.25 --memo "Return payment"
```

#### **Step 7: Verify Privacy Features**
```bash
# Check that all privacy features are applied
./target/release/netcoin-cli info privacy
./target/release/netcoin-cli info network-status
```

#### **Step 8: Multi-Node Testing (Optional)**
```bash
# Deploy additional nodes for consensus testing
./target/release/netcoin-devnet deploy 2
```

### Expected Full Workflow Output

```
🏗️ Initializing Netcoin DevNet...
✅ DevNet node deployed successfully!

⛏️ Starting DevNet mining...
✅ Block 1 mined in 0.00s! 🎉 💰 Reward: 100 NTC added to genesis wallet
✅ Block 2 mined in 0.00s! 🎉 💰 Reward: 100 NTC added to genesis wallet

🔐 Creating new Netcoin wallet...
✅ Wallet created successfully!
📍 Address: @alice_wallet_address

🔐 Creating new Netcoin wallet...
✅ Wallet created successfully!
📍 Address: @bob_wallet_address

Registering alias @alice...
✅ Alias @alice registered successfully!
💰 Registration fee: 0.1 NTC

Registering alias @bob...
✅ Alias @bob registered successfully!
💰 Registration fee: 0.1 NTC

💸 Sending 0.5 NTC from @alice to @bob...
🔐 Privacy Features Applied:
   ✅ MLSAG Ring Signature (16 decoy outputs)
   ✅ Bulletproofs Range Proof (amount validity)
   ✅ Pedersen Commitment (amount hiding)
   ✅ ElGamal Encryption (memo protection)
   ✅ Stealth Address (recipient privacy)
✅ Transaction sent successfully!

Privacy Statistics:
  Ring Signature Size: 16 members
  Confidential Transactions: Enabled
  Stealth Addresses: Enabled
  ElGamal Encryption: IND-CCA2
  @Alias System: Enabled
```

### Testing Checklist

- [ ] ✅ DevNet initializes successfully
- [ ] ✅ Mining creates real blocks with rewards
- [ ] ✅ Wallets create with proper seed phrases
- [ ] ✅ @Alias registration works with balance checks
- [ ] ✅ Privacy transactions send with all 5 features
- [ ] ✅ Network status shows proper statistics
- [ ] ✅ Multi-node deployment works (optional)

---

## 🧪 Automated Testing & Development

### Quick Test Script

Netcoin provides an automated testing script that runs through all DevNet functionalities:

```bash
# Navigate to development tools
cd ../netcoin-internal

# Run complete DevNet integration tests
./scripts/test-devnet.sh

# Run with verbose output
./scripts/test-devnet.sh --verbose

# Keep test data after completion
./scripts/test-devnet.sh --keep-data

# Get help
./scripts/test-devnet.sh --help
```

The script automatically:
- ✅ Builds all required components
- ✅ Initializes DevNet environment
- ✅ Creates test wallets
- ✅ Mines blocks to earn NTC
- ✅ Tests balance checking
- ✅ Sends privacy transactions between wallets
- ✅ Tests @alias system
- ✅ Verifies network status
- ✅ Validates privacy features

### Makefile Commands

Use the provided Makefile for convenient development:

```bash
# Show all available commands
make help

# Build all components
make build

# Build for production
make build-release

# Run unit tests
make test

# Run full DevNet integration tests
make test-devnet

# Initialize DevNet
make devnet-init

# Check DevNet status
make devnet-status

# Clean build artifacts
make clean

# Clean everything including test data
make clean-all
```

### Development Workflow

```bash
# 1. Setup development environment
make build

# 2. Initialize DevNet
make devnet-init

# 3. Run full integration tests
make test-devnet

# 4. Quick manual testing
make create-wallet    # Create a wallet
make mine-test        # Mine to @test-wallet
make check-balance    # Check balance

# 5. View documentation
make serve-docs
```

### CI/CD Integration

The repository includes GitHub Actions for automated testing:

- **Triggers**: Push to main/develop, pull requests
- **Manual Runs**: Via GitHub UI with verbose/keep-data options
- **Artifact Upload**: Test data preserved on failures
- **Caching**: Rust/Python dependencies cached for speed

---

## 🎯 Next Steps

Now that you have a working DevNet:

1. **Run Automated Tests**: Use `./test-devnet.sh` to verify everything works
2. **Explore Privacy Features**: Try different transaction types and amounts
3. **Test @Alias System**: Register multiple aliases, send between them
4. **Multi-Node Testing**: Deploy more nodes and test P2P communication
5. **Performance Testing**: Send many transactions, test limits
6. **Integration Testing**: Connect external applications

## 📚 Additional Resources

- [Netcoin Architecture](../ARCHITECTURE.md)
- [CLI Reference](../CLI.md)
- [Privacy Features](../FEATURES.md)
- [Roadmap](../ROADMAP.md)
- [Makefile](../Makefile) - Development commands
- [test-devnet.sh](../test-devnet.sh) - Automated testing script

---

**Congratulations! You now have a fully functional Netcoin DevNet with privacy transactions, @aliases, and P2P networking. Ready to explore the most advanced privacy cryptocurrency ever built!** 🚀🔐
