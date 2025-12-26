# NetCoin (NTC) Complete User Guide

NetCoin is a revolutionary decentralized network that combines blockchain consensus with global routing infrastructure. Using Proof of Network (PoNW), it creates an energy-backed economy where contributing to the network earns NTC tokens that power premium services.

## What is NetCoin?

NetCoin implements a paradigm shift in blockchain design by making computational energy genuinely productive. Unlike traditional blockchains that waste energy on arbitrary computations, NetCoin embeds proof-of-work puzzles directly into Mycelium's decentralized routing infrastructure.

### Key Innovation: Proof of Network (PoNW)
- **Energy Verification**: Cryptographic proof of actual network routing work
- **Useful Computation**: Every puzzle solved improves global network performance
- **Fair Economy**: Earn NTC proportional to routing contribution
- **Premium Services**: Use earned NTC for QoS routing, VPNs, and secure channels
- **Sustainable Growth**: Network expansion funds itself through participation

## Network Architecture Overview

NetCoin operates as an integrated dual-layer system:

```
┌─────────────────────────────────────┐
│         NetCoin Node Process        │
│    (Single Binary Deployment)       │
├─────────────────────────────────────┤
│ NetCoin Blockchain Engine           │
│ • Privacy transactions (ring sigs)  │
│ • PoNW consensus validation        │
│ • Wallet & alias management         │
├─────────────────────────────────────┤
│ Mycelium Routing Daemon             │
│ • TUN interface (utun/netcoin0)    │
│ • IPv6 overlay networking           │
│ • Packet forwarding & routing       │
│ • Real-time contribution metrics    │
└─────────────────────────────────────┘
```

When you run `netcoin-node start`, you automatically:
- ✅ **Start NetCoin blockchain** (privacy, wallets, consensus)
- ✅ **Launch Mycelium routing daemon** (network participation)
- ✅ **Begin earning NTC** through PoNW mining
- ✅ **Contribute to global network** infrastructure

## User Journey: Complete Participation Guide

### 🎯 **Primary Contributors: Full Node Operators**

#### **Who**: Desktop/Server users with stable internet
#### **Contribution**: Direct routing infrastructure + bandwidth
#### **Rewards**: Maximum NTC earnings + premium access
#### **Requirements**: Desktop/server with stable internet connection

#### **Setup Process:**
```bash
# 1. Install NetCoin
git clone https://github.com/netcoin-ntc/netcoin-core.git
cd netcoin-core && cargo build --release

# 2. Create wallet (24-word seed + optional passphrase)
./target/release/netcoin-node wallet create

# 3. Start node (automatically runs Mycelium routing)
./target/release/netcoin-node node start

# 4. Monitor earnings
./target/release/netcoin-node wallet balance @youraddress
```

#### **What Happens When You Start:**
1. **NetCoin Blockchain**: Initializes privacy-focused ledger
2. **Mycelium Daemon**: Launches routing daemon with TUN interface
3. **Network Participation**: Begins forwarding packets for global network
4. **PoNW Mining**: Generates NTC based on routing contributions
5. **Premium Access**: Earned NTC unlocks QoS routing, VPNs, etc.

#### **Daily Experience:**
- **Earn 50-200 NTC/day** (depending on routing contribution)
- **Automatic routing** in background (low CPU/bandwidth usage)
- **Premium services** access with earned tokens
- **Network governance** participation rights

### 📱 **Secondary Participants: Light Clients & Mobile Users**

#### **Who**: Phone/tablet users, occasional contributors
#### **Contribution**: Network usage validation, light verification
#### **Rewards**: Ecosystem incentives, basic services access
#### **Requirements**: Smartphone/tablet with NetCoin app

#### **Mobile Participation Options:**

##### **The Reality: Mobile Phones Cannot Run Mycelium Routing Daemons**

**Technical Limitation**: Mobile operating systems (iOS/Android) do not allow TUN interfaces required for packet routing. This is a fundamental OS security restriction.

**However: Mobile Users Can Still Contribute Meaningfully!**

##### **Option A: Light Client with Economic Participation (Recommended)**
```bash
# iOS/Android App:
# - Download NetCoin mobile app
# - Create wallet with seed phrase
# - Connect to NetCoin network
# - Use & provide services on Mycelium
# - Earn ecosystem rewards & discounts
```

**Capabilities:**
- ✅ **Wallet management** (create, backup, transactions)
- ✅ **@username aliases** (register and use)
- ✅ **Basic transactions** (privacy-preserving)
- ✅ **Service access** (websites, APIs on Mycelium)
- ✅ **Service hosting** (run websites/APIs using the network)
- ✅ **Governance participation** (vote on network decisions)

**How Mobile Users Contribute to Mycelium Ecosystem:**
- ✅ **Pay for premium services** → Funds network infrastructure & full node operators
- ✅ **Provide services** → Increases network utility (websites, APIs attract more users)
- ✅ **Create demand** → More users → More full nodes → Better network coverage
- ✅ **Economic incentives** → Premium payments subsidize routing infrastructure
- ✅ **Validation support** → Light client verification helps secure the network

**Example Economic Flow:**
```
Mobile User → Pays 10 NTC for premium service
          → Funds Full Node Operator
          → Full Node Operator routes more packets
          → Better network performance
          → More users attracted
          → Network grows sustainably
```

**Limitations:**
- ❌ **Cannot run TUN interface** (iOS/Android OS restrictions)
- ❌ **Cannot forward packets** (battery/network/mobile constraints)
- ❌ **No direct PoNW mining** (insufficient resources for routing daemon)

##### **Option B: Remote Mining (Future)**
- **Delegate routing** to trusted full nodes
- **Earn portion of rewards** from delegated routing
- **Maintain control** through smart contracts
- **Mobile-optimized** participation model

#### **Mobile User Journey:**
1. **Download App** → Create wallet with 24-word seed
2. **Register Alias** → `@yourname` for human-readable addressing
3. **Use Services** → Access ntc:// websites and APIs
4. **Earn Rewards** → Governance tokens, service discounts
5. **Contribute** → Network validation and light verification

### 🏢 **Enterprise Participants: Business Deployments**

#### **Who**: Companies, organizations, institutions
#### **Contribution**: Corporate network infrastructure
#### **Rewards**: NTC from organizational routing + enterprise features
#### **Requirements**: Server infrastructure, corporate IT approval

#### **Enterprise Setup:**
```bash
# Deploy on corporate servers
docker run -d --name netcoin-enterprise \
  -v /corporate/data:/data \
  netcoin-core:latest \
  --enterprise-mode \
  --routing-capacity 100mbps

# Corporate benefits:
# - NTC earnings from company network usage
# - Premium SLA guarantees
# - Enterprise compliance features
# - Multi-signature wallet support
# - Audit trails and reporting
```

#### **Enterprise Advantages:**
- ✅ **Organizational Earnings**: NTC from company routing capacity
- ✅ **Premium SLAs**: Guaranteed QoS for critical traffic
- ✅ **Compliance Ready**: Regulatory compliance features
- ✅ **Multi-User**: Team wallet management
- ✅ **Corporate Governance**: Enterprise voting rights

## Earning NTC: The Complete Economics Guide

### 💰 **Primary Earnings: Full Node Routing**

#### **How It Works:**
1. **Run NetCoin Node** → Launches Mycelium routing daemon
2. **Forward Packets** → Contribute bandwidth to global network
3. **Generate Proofs** → Cryptographic verification of routing work
4. **Earn NTC** → Proportional to verified contribution
5. **Compound Growth** → Better network = more users = more value

#### **Earnings Factors:**
- **Bandwidth Contribution**: Higher bandwidth = more routing = more NTC
- **Network Position**: Strategic routing position increases earnings
- **Uptime**: Consistent participation maximizes rewards
- **Network Health**: Contributing to healthy network = premium rewards

#### **Typical Earnings (Estimated):**
- **Home User**: 50-200 NTC/day (10-50 USD at launch)
- **Small Business**: 500-2000 NTC/day (100-500 USD)
- **Enterprise**: 5000+ NTC/day (1000+ USD)

### 🎁 **Secondary Earnings: Ecosystem Rewards**

#### **Mobile Users:**
- **Governance Tokens**: Participate in network decisions
- **Service Discounts**: Reduced fees for premium services
- **Referral Bonuses**: Earn from bringing new users
- **Staking Rewards**: Lock NTC for additional returns

#### **Service Providers:**
- **Hosting Fees**: Charge for premium service access
- **API Monetization**: Revenue from service usage
- **Market Making**: Provide liquidity in NTC markets

### 🔄 **Service Economy: Using Your NTC**

#### **Premium Routing Services:**
```bash
# QoS Routing (guaranteed bandwidth)
netcoin-node service request-qos --bandwidth 100mbps --duration 24h

# VPN Tunnels (encrypted corporate connections)
netcoin-node service create-vpn --endpoint @partner --encryption aes256

# Secure Channels (end-to-end encrypted communication)
netcoin-node service secure-channel @colleague --protocol video
```

#### **Domain & Service Registration:**
```bash
# Register .ntc domain
netcoin-node domain register company.ntc 1000000000  # 100 NTC burn

# Create service endpoints
netcoin-node domain register-service api company.ntc 100000000  # 1 NTC burn
netcoin-node domain register-service website company.ntc 100000000

# Access via Mycelium
# ntc://api.company.ntc/v1/data
# ntc://website.company.ntc/
```

## Technical Requirements & Compatibility

### 💻 **Full Node Requirements:**
- **OS**: Linux, macOS, Windows (TUN support required)
- **CPU**: 2+ cores (routing optimization)
- **RAM**: 4GB+ (blockchain + routing state)
- **Storage**: 100GB+ SSD (blockchain growth)
- **Network**: 10Mbps+ stable connection
- **Power**: 24/7 uptime for maximum earnings

### 📱 **Mobile Requirements:**
- **OS**: iOS 14+, Android 10+
- **Storage**: 500MB+ available space
- **Network**: 3G+ for basic functionality
- **Battery**: Optimized for mobile usage

### 🏢 **Enterprise Requirements:**
- **Infrastructure**: Dedicated servers/containers
- **Network**: Corporate bandwidth allocation
- **Security**: Enterprise-grade compliance
- **Monitoring**: 24/7 operational oversight

## Getting Started: Step-by-Step

### 🚀 **Quick Start (5 minutes):**
```bash
# 1. Get NetCoin
git clone https://github.com/netcoin-ntc/netcoin-core.git
cd netcoin-core && make build

# 2. Create secure wallet
./target/release/netcoin-node wallet create
# → Save the 24-word seed phrase!

# 3. Start earning NTC
./target/release/netcoin-node node start
# → Automatically begins routing and mining

# 4. Check your earnings
./target/release/netcoin-node wallet balance @youraddress
```

### 📋 **Complete Setup Checklist:**

#### **Wallet Security:**
- [ ] Generate 24-word seed phrase
- [ ] Set optional passphrase for extra security
- [ ] Backup seed phrase in multiple secure locations
- [ ] Test wallet recovery with backup phrase

#### **Node Configuration:**
- [ ] Choose appropriate network mode (home/business/enterprise)
- [ ] Configure routing capacity allocation
- [ ] Set up monitoring and alerts
- [ ] Enable automatic updates

#### **Service Integration:**
- [ ] Register @username alias (0.1 NTC)
- [ ] Set up premium service subscriptions
- [ ] Configure enterprise features (if applicable)
- [ ] Join governance participation

## Security & Privacy

### 🔐 **Privacy by Design:**
- **Ring Signatures**: All transactions private by default
- **One-Time Addresses**: Recipient privacy protection
- **Mycelium Encryption**: End-to-end encrypted routing
- **Zero-Knowledge Proofs**: Selective disclosure capabilities

### 🛡️ **Network Security:**
- **Cryptographic Verification**: All routing work mathematically proven
- **Consensus Validation**: Network agreement on contribution claims
- **Sybil Resistance**: Economic barriers to fake participation
- **Fraud Prevention**: Automatic detection and slashing

### 💰 **Economic Security:**
- **Inflation Control**: Service burning mechanisms
- **Value Accrual**: Network growth drives NTC appreciation
- **Fair Distribution**: Proportional rewards for contribution
- **Sustainable Model**: Infrastructure funds itself

## Community & Support

### 📚 **Learning Resources:**
- **Documentation**: Complete technical guides
- **Tutorials**: Step-by-step setup instructions
- **Video Guides**: Visual walkthroughs
- **Community Forum**: User discussions and support

### 🤝 **Getting Help:**
- **GitHub Issues**: Bug reports and technical issues
- **Community Discord**: Real-time user support
- **Developer Docs**: API references and integration guides
- **Enterprise Support**: Commercial assistance available

### 🌍 **Contributing:**
- **Code Contributions**: Rust development opportunities
- **Documentation**: Help improve user guides
- **Community Building**: Organize local meetups
- **Translation**: Multi-language support

---

**NetCoin: Where running a node means building the future internet infrastructure - and getting paid to do it.**

**Ready to start earning NTC and contributing to the decentralized internet?** 🚀⚡🌐
