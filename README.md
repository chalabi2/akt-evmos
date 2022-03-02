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
    image: chandrastation/evmosakt:v1.0.0-testnet
    env:
      - MONIKER=akt_evmos
      - CHAIN_JSON=https://raw.githubusercontent.com/chalabi2/chain-registry/master/evmos/chain-testnet.json
      - VALIDATE_GENESIS=0
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
