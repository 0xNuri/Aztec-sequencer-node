# Aztec-sequencer-node

Aztec Sequencer Node Setup Guide

Welcome, aspiring Node Operator!

You stand at the gateway to the Network — the threshold where sequencers are forged.
3
🛠️ Your first task: become an Apprentice.
Prove your mettle. Show the Network you can carry the sacred spark.


If you succeed, you'll rise to Guardian.

Those with mastery may even ascend to Defender status.


And if, by some divine accident, you encounter a Sentinel —

drop to your knees immediately and worship at the feet of a node operator god.




🧱️ What's Your Role?

The Aztec sequencer node is critical infrastructure.

It orders transactions, produces blocks, and keeps the zk magic alive.

Before a block can be published, it must be verified by a validator committee.

These validators re-execute the transactions and sign off on validity.

Once 2/3 + 1 signatures are gathered, the sequencer submits it to L1.

Meanwhile, the archiver monitors L1, stores history, and helps sync new nodes.






🛠️ Prerequisites

OS: Linux/macOS

RAM: 16GB

CPU: 8 cores

Disk: 1TB SSD

Bandwidth: 25 Mbps

Sepolia ETH: For gas (get it from faucets or Discord)

Ports: Forward TCP + UDP 40400

IP: Pass external IP to --p2p.p2pIp

Keys:

ETH private key (for posting blocks)
ETH address (to receive rewards)







🔧 Run Your Sequencer


aztec start --node --archiver --sequencer \

  --network alpha-testnet \
  
  --l1-rpc-urls https://example.com \
  
  --l1-consensus-host-urls https://example.com \
  
  --sequencer.validatorPrivateKey 0xYourPrivateKey \
  
  --sequencer.coinbase 0xYourAddress \
  
  --p2p.p2pIp 999.99.999.99







🔑 Register as a Validator

Once fully synced, register with:

aztec add-l1-validator \

  --l1-rpc-urls https://eth-sepolia.g.example.com/example/your-key \
  
  --private-key your-private-key \
  
  --attester your-validator-address \
  
  --proposer-eoa your-validator-address \
  
  --staking-asset-handler 0xF739D03e98e23A7B65940848aBA8921fF3bAc4b2 \
  
  --l1-chain-id 11155111






🐫 Docker Compose Setup


services:
  network_mode: host
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
    volumwes:
     - /home/my-node/node:/data
  







🧪 Troubleshooting


Use host.docker.internal for local L1 access (Mac/Windows)

Use network_mode: host for Linux

Confirm your L1 clients (e.g., Geth, Reth) are accessible

Only Geth and Reth are confirmed to work reliably

Join the Aztec Discord for support


🔥 The chain awaits. Let's see what you're made of.
