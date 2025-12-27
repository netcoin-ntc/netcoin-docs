# Netcoin DevNet Complete Guide: From Zero to Privacy Transactions

This comprehensive guide walks you through deploying and using Netcoin's DevNet - a development environment for testing all Netcoin features with accelerated parameters for rapid iteration.

## Table of Contents

- [Prerequisites](#prerequisites)
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
git clone https://github.com/your-org/netcoin-ntc.git
cd netcoin-ntc/netcoin-core

# Install Rust (if not already installed)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env

# Build all binaries
cargo build --release
```

## DevNet Architecture

### DevNet Parameters
| Parameter | DevNet Value | MainNet Value | Purpose |
|-----------|-------------|---------------|---------|
| Block Time | 30 seconds | 10 minutes | Rapid testing |
| Mining Difficulty | 1 | Variable | Easy mining |
| Genesis Allocation | 1000 NTC | 0 NTC | Testing funds |
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
   💰 Genesis Allocation: 1000 NTC
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
   💰 Genesis Allocation: 1000 NTC
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
  └── ...               # Future blockchain data
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
   📊 Amount: 0.5 NTC (500000000 satoshis)
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
   💰 Genesis Allocation: 1000 NTC
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
   • TCP-based peer connections
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
| **Genesis Allocation** | 1000 NTC | 0 NTC |
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

## 🎯 Next Steps

Now that you have a working DevNet:

1. **Explore Privacy Features**: Try different transaction types
2. **Test @Alias System**: Register multiple aliases, send between them
3. **Multi-Node Testing**: Deploy more nodes and test P2P communication
4. **Performance Testing**: Send many transactions, test limits
5. **Integration Testing**: Connect external applications

## 📚 Additional Resources

- [Netcoin Architecture](../ARCHITECTURE.md)
- [CLI Reference](../CLI.md)
- [Privacy Features](../FEATURES.md)
- [Roadmap](../ROADMAP.md)

---

**Congratulations! You now have a fully functional Netcoin DevNet with privacy transactions, @aliases, and P2P networking. Ready to explore the most advanced privacy cryptocurrency ever built!** 🚀🔐
