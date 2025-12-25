# Netcoin CLI Reference

Netcoin provides a comprehensive command-line interface for wallet management, alias operations, and node control.

## Getting Started

After building Netcoin:

```bash
cd netcoin
./target/release/netcoin-node --help
```

## Commands

### Node Commands

#### `netcoin-node node`
Start the Netcoin node for mining and network participation.

```bash
netcoin-node node
```

This starts:
- PoNW mining with routing puzzles
- Blockchain synchronization
- Peer connections (future)
- NTC generation

#### `netcoin-node info`
Display network and node information.

```bash
netcoin-node info
```

Output:
```
Netcoin (NTC) - PoNW Blockchain
Version: 0.1.0
Consensus: Proof of Network
Network: 0x500::/7 subnet
```

### Wallet Commands

#### `netcoin-node wallet create`
Create a new wallet with a unique address.

```bash
netcoin-node wallet create
```

Output:
```
Created wallet with address: @298ba6a93c018566e69c6cf6291399fd959e1e6d273356b3f5a0f3f8d707e5ee
```

#### `netcoin-node wallet balance <address>`
Check the NTC balance of an address.

```bash
netcoin-node wallet balance @298ba6a93c018566e69c6cf6291399fd959e1e6d273356b3f5a0f3f8d707e5ee
```

Output:
```
Balance for @298ba6a93c...: 0 NTC (UTxO implementation needed)
```

#### `netcoin-node wallet send <to> <amount>`
Send NTC to another address.

```bash
netcoin-node wallet send @recipient_address 100
```

Output:
```
Created transaction: 100 NTC to @recipient_address
```

### Alias Commands

#### `netcoin-node wallet check-alias <alias>`
Check if an alias is available or registered.

```bash
netcoin-node wallet check-alias myname
```

Available alias:
```
Alias @myname is available
```

Registered alias:
```
Alias @myname is registered to @wallet_address
```

#### `netcoin-node wallet register-alias <alias> <payment>`
Register a premium alias by paying NTC.

```bash
netcoin-node wallet register-alias myname 100
```

Success:
```
Successfully registered alias @myname for 100 NTC
```

Already taken:
```
Alias @myname is already taken
```

## Examples

### Complete User Flow

1. **Create wallet**:
```bash
$ netcoin-node wallet create
Created wallet with address: @298ba6a93c018566e69c6cf6291399fd959e1e6d273356b3f5a0f3f8d707e5ee
```

2. **Start node to earn NTC**:
```bash
$ netcoin-node node &
```

3. **Check alias availability**:
```bash
$ netcoin-node wallet check-alias johnsmith
Alias @johnsmith is available
```

4. **Register premium alias**:
```bash
$ netcoin-node wallet register-alias johnsmith 100
Successfully registered alias @johnsmith for 100 NTC
```

5. **Send to alias**:
```bash
$ netcoin-node wallet send @johnsmith 50
Created transaction: 50 NTC to @johnsmith
```

## Technical Details

### Address Format
- **Free addresses**: `@` + 64-character hex hash
- **Premium aliases**: `@` + custom name (paid)

### Storage
- Wallets stored in `./netcoin_data/` directory
- RocksDB for persistent blockchain and alias registry
- Encrypted private keys (placeholder for production)

### Error Handling
- Invalid addresses return clear error messages
- Insufficient balance shows current balance
- Network errors display connection status

### Future Commands
- `netcoin-node wallet list` - List all saved wallets
- `netcoin-node wallet import <key>` - Import wallet from private key
- `netcoin-node wallet export <address>` - Export wallet backup
- `netcoin-node network status` - Show network statistics
- `netcoin-node transaction history <address>` - View transaction history

## Troubleshooting

### Common Issues

**"Permission denied" when running node**
- Ensure you have write access to `./netcoin_data/`
- Check if another instance is running

**"Alias already taken"**
- Choose a different alias name
- Check availability first with `check-alias`

**"UTxO implementation needed" for balance**
- Balance checking requires full transaction system
- Currently shows placeholder until Phase 2 completion

### Logs and Debugging

Enable verbose logging:
```bash
RUST_LOG=debug netcoin-node node
```

Check data directory:
```bash
ls -la ./netcoin_data/
```

## Security Notes

- **Private keys** are stored encrypted (placeholder)
- **Alias payments** are verified but not yet deducted from balances
- **Transactions** are created but not broadcast (P2P needed)
- Use testnet for experimentation, mainnet for production
