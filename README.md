# Aztec Sequencer Node Setup Guide

Welcome, aspiring Node Operator!  
You stand at the gateway to the Network — *the threshold where sequencers are forged.*

## Your First Task: Become an Apprentice

Prove your mettle. Show the Network you can carry the sacred spark.

**If you succeed, you’ll rise to Guardian.**  
Those with mastery may even ascend to *Defender status.*

And if, by some divine accident, you encounter a *Sentinel*—  
drop to your knees immediately and worship at the feet of a **node operator god**.

To earn your Apprentice role, you must demonstrate the fundamentals.  
Your journey begins with setting up a sequencer node.  
Even if you can’t register yet, don’t worry — just get it up and syncing.

Once your node is running and synced, use the following command to prove your worth and *claim your Apprentice title*.

---

## Quickstart

### 1. Setup Your Node

You only need to get through the **Start Your Sequencer** command to get your node running:  
[Aztec Sequencer Setup Guide](https://docs.aztec.network/the_aztec_network/guides/run_nodes/how_to_run_sequencer)

### 2. Get Info from Your Node
```bash
/operator help
```

### 3. Prove You Are in Sync
```bash
/operator start
```

---

## Hardware Requirements

- **Bandwidth:** 25 Mbps up/down  
- **CPU:** 8-core  
- **RAM:** 16 GiB  
- **Storage:** 1 TB SSD  

---

## Core Concepts

### What Does the Sequencer Do?

The Aztec sequencer node is responsible for:

- Ordering transactions  
- Producing blocks  
- Validating transactions with other sequencer nodes  
- Submitting valid blocks to Ethereum Layer 1

### Archiver Component

Maintains historical chain data by:

- Monitoring L1 for new blocks  
- Managing contract data and L1-to-L2 messages  
- Ensuring chain state sync and availability

---

## Prerequisites

- Linux or macOS with terminal access  
- Aztec tool installed  
- Aztec testnet version set with:
```bash
aztec-up alpha-testnet
```

- Join the [Aztec Discord](https://discord.gg/aztec) for community support.

---

## Boot Your Sequencer

### Required Resources

- **L1 Execution Client RPCs:** Use Alchemy, Infura, or run Geth/Nethermind  
- **L1 Consensus RPCs:** Use QuickNode, dRPC, or other verified consensus endpoints  
- **Ethereum Keys:** Private key (`--sequencer.validatorPrivateKey`) and public address (`--sequencer.coinbase`)  
- **Networking:** Port forwarding (UDP + TCP) on port `40400`  
- **Sepolia ETH:** Use [faucets](https://sepolia-faucet.pk910.de/) or ask in Discord

### Launch Command
```bash
aztec start --node --archiver --sequencer   --network alpha-testnet   --l1-rpc-urls https://example.com   --l1-consensus-host-urls https://example.com   --sequencer.validatorPrivateKey 0xYourPrivateKey   --sequencer.coinbase 0xYourAddress   --p2p.p2pIp 999.99.999.99
```

---

## Register as a Validator

Once synced, register with:
```bash
aztec add-l1-validator   --l1-rpc-urls https://eth-sepolia.g.example.com/example/your-key   --private-key your-private-key   --attester your-validator-address   --proposer-eoa your-validator-address   --staking-asset-handler 0xF739D03e98e23A7B65940848aBA8921fF3bAc4b2   --l1-chain-id 11155111
```

---

## Docker Compose Setup

```yaml
name: aztec-node
services:
  node:
    image: aztecprotocol/aztec:0.85.0-alpha-testnet.5
    environment:
      ETHEREUM_HOSTS: ""
      L1_CONSENSUS_HOST_URLS: ""
      DATA_DIRECTORY: /data
      VALIDATOR_PRIVATE_KEY: $VALIDATOR_PRIVATE_KEY
      P2P_IP: $P2P_IP
      LOG_LEVEL: debug
    entrypoint: >
      sh -c 'node --no-warnings /usr/src/yarn-project/aztec/dest/bin/index.js start --network alpha-testnet start --node --archiver --sequencer'
    ports:
      - 40400:40400/tcp
      - 40400:40400/udp
      - 8080:8080
    volumes:
      - /home/my-node/node:/data
    network_mode: host
```

---

## Troubleshooting

### Docker Can’t Reach Localhost?

**Use:** `host.docker.internal`  
**Or:** Add `network_mode: "host"` (Linux only)

### Run Your Own Sepolia Node?

Only **geth** and **reth** are confirmed to work reliably.

---

## Final Words

**The chain awaits. Let’s see what you’re made of.**  
Happy Sequencing!


🔥 The chain awaits. Let's see what you're made of.
Here's your cleaned-up and properly spaced GitHub-style README. It's now ready for publishing. Let me know if you want sections added (e.g., FAQs, visuals, tips for debugging).
