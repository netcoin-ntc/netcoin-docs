# NetCoin Architecture

## High-Level Overview

NetCoin is a decentralized network combining blockchain consensus with overlay networking. It uses PoNW (Proof of Network) to create an energy-backed economy where routing work generates tokens.

```
┌─────────────────┐    ┌─────────────────┐
│   NetCoin Node  │    │   Mycelium      │
│                 │    │   Routing       │
│ ┌─────────────┐ │    │                 │
│ │  PoN        │◄┼───►│ Babel Protocol │
│ │ Consensus   │ │    │ + PoW Puzzles  │
│ └─────────────┘ │    │                 │
│                 │    │ Overlay Network │
│ ┌─────────────┐ │    │ (0x500::/7)    │
│ │ NTC Wallet  │ │    └─────────────────┘
│ └─────────────┘ │
└─────────────────┘
         │
         ▼
   Premium Services
   (QoS, VPN, etc.)
```

## Components

### 1. Mycelium Integration
- **Modified Mycelium**: Forked to embed PoW in routing decisions
- **PoW Module**: Solves puzzles based on routing data
- **Subnet**: 0x500::/7 (separate from standard Mycelium's 0x400::/7)

### 2. PoN Consensus
- **Blockchain**: Rust implementation with blocks validated by routing puzzles
- **PoW Puzzles**: Nonce-finding tied to packet forwarding data
- **Rewards**: NTC earned proportional to energy spent on routing

### 3. Client Software
- **Node Types**:
  - Full nodes: 24/7 routing + consensus
  - Light nodes: Opportunistic participation
  - Consumers: Access via free basic + NTC premium
- **Wallet**: Built-in NTC management with @aliases

### 4. Network Services
- **Basic**: Standard routing (free)
- **Premium**: QoS, VPN, bandwidth boost (NTC-paid)

## Data Flow

1. **Packet Arrival**: Node receives data packet
2. **Routing Decision**: Mycelium selects path, solves PoW puzzle
3. **Validation**: PoW success proves energy, updates routing table
4. **Forwarding**: Packet sent via chosen route
5. **Rewards**: Successful routing earns NTC

## Security Model

- **Energy Barriers**: PoW puzzles scale difficulty with network size
- **Sybil Resistance**: New nodes must prove routing energy
- **DDoS Protection**: Distributed routing absorbs attacks

## Deployment

- **Docker Compose**: Orchestrates Mycelium + NetCoin
- **Cross-Platform**: Runs on any OS with Docker
- **Scalability**: Light clients enable mobile participation

## Future Extensions

- **Hardware Acceleration**: GPU/ASIC optimization for PoW
- **Zero-Knowledge Proofs**: Enhanced privacy
- **Cross-Chain**: Interoperability with other blockchains
