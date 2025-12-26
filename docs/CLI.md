# Netcoin CLI Reference

Netcoin provides a comprehensive command-line interface for wallet management, privacy features, mining operations, and node control. All commands support privacy by default.

## Getting Started

After building Netcoin:

```bash
cd netcoin-core
./target/release/netcoin-wallet --help
./target/release/netcoin-miner --help
./target/release/netcoind --help
```

## Core Commands

### Wallet Management

#### `netcoin-wallet create`
Create a new privacy-focused wallet with stealth addresses.

```bash
netcoin-wallet create --label "My Main Wallet"
```

Output:
```
Wallet created successfully!
Address: @stealth_7a9b2c5d8e1f4g3h6i9j0k2l5m8n1o4p7q3r6s9t0u
View Key: vkey_3a7b9c2d5e8f1g4h6i0j3k5l8m1n4o7p2q5r8s0t3u6v9w
Seed Phrase: word1 word2 word3 ... word24
⚠️  Backup your seed phrase securely!
```

#### `netcoin-wallet balance`
Check your wallet balance.

```bash
netcoin-wallet balance
```

Output:
```
Wallet Balance (@stealth_...)
Confirmed: 1250.50 NTC
Pending: 0.00 NTC
Unconfirmed: 25.75 NTC
```

#### `netcoin-wallet send`
Send a private transaction with full anonymity.

```bash
# Send with maximum privacy
netcoin-wallet send @alice 100 \
  --privacy maximum \
  --ring-size 16 \
  --memo "Payment for services" \
  --fee auto
```

Output:
```
Transaction created successfully!
TXID: 8f2a9b5c7d1e3f6g9h0i2j4k5l7m8n1o3p5q7r9s2t4u6v8w0x
Privacy Level: Maximum (16-ring MLSAG + Confidential Amounts)
Fee: 0.001 NTC
Confirmations: 0 (pending)
```

#### `netcoin-wallet receive`
Generate a fresh stealth address for receiving payments.

```bash
netcoin-wallet receive --label "Freelance Payment"
```

Output:
```
Fresh stealth address generated:
@stealth_new_2b4c6d8e0f1g3h5i7j9k1l3m5n7o9p1q3r5s7t9u1v3w5x7y9z
This address can only be used once for privacy.
```

#### `netcoin-wallet alias`
Manage human-readable aliases.

```bash
# Register an alias
netcoin-wallet alias register alice 100

# Check availability
netcoin-wallet alias check bob

# Resolve alias to address
netcoin-wallet alias resolve @alice
```

### Mining Operations

#### `netcoin-miner start`
Start CPU mining with RandomX algorithm.

```bash
# Solo mining
netcoin-miner start --threads 8

# Pool mining
netcoin-miner start --pool pool.netcoin.org:3333 --user @youraddress
```

Output:
```
Netcoin CPU Miner v1.0.0
Using RandomX algorithm
Threads: 8
Hashrate: 12.5 KH/s
Difficulty: 1,234,567
Block found! Reward: 100 NTC
```

#### `netcoin-miner status`
Monitor mining performance.

```bash
netcoin-miner status
```

Output:
```
Mining Status
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
State: Active
Algorithm: RandomX
Threads: 8
Hashrate: 12,450 H/s
Difficulty: 1,234,567
Shares: 45/2 (accepted/rejected)
Uptime: 2h 15m 30s
Earnings Today: 125.50 NTC
Power Usage: 125W
Efficiency: 99.6 NTC/kWh
```

#### `netcoin-miner benchmark`
Benchmark your CPU mining performance.

```bash
netcoin-miner benchmark --threads 4 --duration 60
```

Output:
```
RandomX Benchmark Results
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Threads: 4
Duration: 60 seconds
Average Hashrate: 6,250 H/s
Peak Hashrate: 6,890 H/s
CPU Usage: 95%
Memory Usage: 3.8 GB
Efficiency Score: 98.2/100
```

### Node Operations

#### `netcoind`
Run a full Netcoin node.

```bash
# Full node with mining
netcoind --mining --threads 4 --rpc

# Light node for development
netcoind --light --rpc-port 8332

# Testnet node
netcoind --testnet --data-dir ./testnet-data
```

#### `netcoind status`
Check node synchronization and network status.

```bash
netcoind status
```

Output:
```
Netcoin Node Status
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Version: 1.0.0
Network: Mainnet
Block Height: 45,231
Difficulty: 1,234,567,890
Hashrate: 2.3 GH/s
Peers: 127
Sync Status: 100% (up to date)
Mempool: 1,247 transactions
Mining: Active (12.5 KH/s)
```

#### `netcoind getblock`
Retrieve block information.

```bash
# Get latest block
netcoind getblock latest

# Get specific block
netcoind getblock 45231

# Get block with transactions
netcoind getblock 45231 --verbose
```

## Privacy Commands

### Ring Signature Configuration

#### `netcoin-wallet ring`
Manage ring signature settings for enhanced privacy.

```bash
# Set default ring size
netcoin-wallet ring size 16

# View available ring members
netcoin-wallet ring members

# Force refresh ring data
netcoin-wallet ring refresh
```

### Confidential Transactions

#### `netcoin-wallet confidential`
Configure amount hiding settings.

```bash
# Enable confidential amounts
netcoin-wallet confidential enable

# Check confidential transaction support
netcoin-wallet confidential status

# View amount commitments
netcoin-wallet confidential commitments
```

### View Keys

#### `netcoin-wallet view`
Manage view keys for selective transaction sharing.

```bash
# Export view key
netcoin-wallet view export > view_key.txt

# Import view key (read-only access)
netcoin-wallet view import < view_key.txt

# Scan for transactions with view key
netcoin-wallet view scan
```

## Advanced Commands

### Developer Tools

#### `netcoin-wallet dev`
Development and debugging commands.

```bash
# Generate test transactions
netcoin-wallet dev generate-tx --count 100

# Analyze privacy metrics
netcoin-wallet dev privacy-stats

# Export wallet data for analysis
netcoin-wallet dev export-data
```

#### `netcoind dev`
Node debugging and analysis.

```bash
# Analyze blockchain
netcoind dev blockchain-analyze

# Performance profiling
netcoind dev profile --duration 300

# Network debugging
netcoind dev network-debug
```

### Batch Operations

#### `netcoin-wallet batch`
Process multiple transactions.

```bash
# Bulk send
netcoin-wallet batch send recipients.csv

# Bulk alias registration
netcoin-wallet batch alias register aliases.csv
```

## Configuration

### Wallet Configuration
Create `~/.netcoin/wallet.toml`:

```toml
[wallet]
default_privacy = "maximum"
default_ring_size = 16
auto_backup = true
backup_interval = "24h"

[mining]
enabled = false
threads = 8
pool = "pool.netcoin.org:3333"

[network]
rpc_url = "http://localhost:8332"
timeout = 30
retries = 3
```

### Node Configuration
Create `~/.netcoin/netcoind.toml`:

```toml
[node]
data_dir = "~/.netcoin/data"
log_level = "info"
max_peers = 125

[mining]
enabled = true
threads = 8
miner_address = "@your_address"

[network]
port = 8333
rpc_port = 8332
external_ip = "auto"

[privacy]
default_ring_size = 16
confidential_tx = true
elgamal_memos = true
```

## Examples

### Complete Privacy Workflow

1. **Setup Privacy Wallet**:
```bash
$ netcoin-wallet create --privacy
Wallet created with stealth addresses enabled
```

2. **Generate Fresh Receive Address**:
```bash
$ netcoin-wallet receive
@stealth_fresh_7a9b2c5d8e1f4g3h6i9j0k2l5m8n1o4p7q3r6s9t0u
```

3. **Send Anonymous Transaction**:
```bash
$ netcoin-wallet send @recipient 500 \
  --privacy maximum \
  --ring-size 16 \
  --confidential \
  --memo "Encrypted payment note"
Transaction sent anonymously
```

4. **Monitor Mining Rewards**:
```bash
$ netcoin-miner status
Hashrate: 15.2 KH/s | Earnings: 245 NTC today
```

### Exchange Integration

1. **Generate Deposit Address**:
```bash
$ netcoin-wallet exchange deposit
Deposit Address: @exchange_deposit_2b4c6d8e0f1g3h5i7j9k1l3m5n7o9p1q3r5s7t9u1v3w5x7y9z
```

2. **Monitor Deposits**:
```bash
$ netcoin-wallet exchange deposits
Deposit 1: 1000 NTC (confirmed)
Deposit 2: 500 NTC (pending)
```

3. **Prepare Withdrawal**:
```bash
$ netcoin-wallet exchange withdraw @user_address 750 --privacy high
Withdrawal prepared with ring signature privacy
```

## Error Handling

### Common Issues

**"Insufficient ring members"**
```bash
# Solution: Wait for more blockchain data or reduce ring size
netcoin-wallet ring refresh
netcoin-wallet send @recipient 100 --ring-size 8
```

**"Mining not profitable"**
```bash
# Solution: Check current difficulty and earnings
netcoin-miner status
# Consider pool mining for more consistent rewards
netcoin-miner start --pool
```

**"Transaction failed: double spend"**
```bash
# Solution: Check for conflicting transactions
netcoin-wallet history
# Wait for confirmation or use different inputs
```

### Debugging

Enable verbose logging:
```bash
RUST_LOG=netcoin=debug netcoin-wallet balance
RUST_LOG=netcoin=trace netcoind
```

Check logs:
```bash
tail -f ~/.netcoin/logs/netcoin.log
```

## Security Best Practices

- **Always backup** your 24-word seed phrase
- **Use fresh addresses** for each receive (stealth addresses automate this)
- **Enable maximum privacy** for sensitive transactions
- **Verify transactions** before confirming large amounts
- **Keep software updated** for latest security patches

## API Reference

### RPC Interface
Netcoin provides a JSON-RPC interface for advanced integrations:

```bash
# Get blockchain info
curl -X POST http://localhost:8332 \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","method":"getblockchaininfo","params":[],"id":1}'

# Send transaction
curl -X POST http://localhost:8332 \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","method":"sendrawtransaction","params":[tx_hex],"id":2}'
```

### Available RPC Methods
- `getblockchaininfo` - Blockchain statistics
- `getblock` - Block details
- `getrawtransaction` - Transaction data
- `sendrawtransaction` - Broadcast transaction
- `getbalance` - Address balance
- `listtransactions` - Transaction history

## Future Commands

The CLI will expand with additional features:
- **Hardware wallet support**
- **Multi-signature wallets**
- **Batch transaction processing**
- **Advanced privacy analytics**
- **Decentralized exchange integration**

## Support

- **Documentation**: https://netcoin-ntc.github.io/netcoin-docs/
- **GitHub Issues**: https://github.com/netcoin-ntc/netcoin-core/issues
- **Community Forum**: https://community.netcoin.org
- **Discord**: https://discord.gg/netcoin

---

**Netcoin CLI provides powerful privacy-preserving tools for managing your cryptocurrency. All commands default to maximum privacy to protect your financial sovereignty.**
