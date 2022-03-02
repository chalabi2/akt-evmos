# EVMOS on AKT
A simple guide on deploying an evmos node on Akash. Forked from Ovrclk/Cosmos-Omnibus 

### Cosmos-Omnibus

Omnibus allows us to setup simple environment variables in the deploy file in order to create Validator Infrastructure, RPC Nodes, or any other configuration for a Cosmos Node

## Guide 

* Step 1) Download [Akashlytics](https://akashlytics.com/deploy)
* Step 2) copy and paste the deploy file below for a simple RPC node configuration

### Deploy FIle

Located in the main repo is are multiple deployment files to use on Akashlytics. Each deployment file is named after a simple node configuration. Here is the RPC config

```bash
---
version: "2.0"

services:
  node:
    image: chandrastation/evmosakt:v1.4.0-testnet
    env:
      - MONIKER=akt_evmos
      - CHAIN_ID=evmos_9000-3
      - VALIDATE_GENESIS=0
      - P2P_PERSISTENT_PEERS=c00ec5f0c8d664e5eccdb312a7394f16b325e725@bd-evmos-testnet-sentry-01.bdnodes.net:26656,68c0966f3f6ee42369710d57de2e015ec87b36ca@bd-evmos-testnet-sentry-02.bdnodes.net:26656,8d1a0934d38f09e587cca498c9f552abf3258806@bd-evmos-testnet-sentry-03.bdnodes.net:26656,3a6b22e1569d9f85e9e97d1d204a1c457d860926@bd-evmos-testnet-seed-node-01.bdnodes.net:26656,c10c7be0e6b4a1721cffa6a10a24a8c8ec94bb82@34.133.158.107:26656,36cd75ae8a87e24f5c16cda8a2de8c0959678e9f@35.232.93.147:26656,b7cd1af9540271e851890c0ac009e0039558addf@34.77.4.52:26656,f53a5d262d7f502894e8d19d179afe156eeb812b@34.140.141.181:26656,c00ec5f0c8d664e5eccdb312a7394f16b325e725@34.85.200.127:26656,8d1a0934d38f09e587cca498c9f552abf3258806@34.76.223.126:26656,68c0966f3f6ee42369710d57de2e015ec87b36ca@35.203.156.214:26656
      - GENESIS_URL=https://github.com/tharsis/testnets/raw/main/evmos_9000-3/genesis.zip
    expose:
      - port: 26657
        as: 80
        to:
          - global: true
      - port: 26656
        to:
          - global: true

profiles:
  compute:
    node:
      resources:
        cpu:
          units: 2
        memory:
          size: 8Gi
        storage:
          size: 100Gi
  placement:
    dcloud:
      attributes:
        host: akash
      signedBy:
        anyOf:
          - akash1365yvmc4s7awdyj3n2sav7xfx76adc6dnmlx63
      pricing:
        node:
          denom: uakt
          amount: 100

deployment:
  node:
    dcloud:
      profile: node
      count: 1
```
* Step 3) click through the deployment transactions

### Interaction
Connecting to the RPC or utilizing the Akash deployed node as a peer is as easy as adding the node id (printed in the logs) and Akash URI to a typical node config.toml file. Further configuration can be found at the [Omni-Bus Repo](https://github.com/ovrclk/cosmos-omnibus)
