# EVMOS on AKT
A simple guide on deploying an evmos node on Akash. Forked from Ovrclk/Cosmos-Omnibus 

### [Cosmos-Omnibus](https://github.com/ovrclk/cosmos-omnibus)

Omnibus allows us to setup simple environment variables in an Akash deployment file in order to create Validator Infrastructure, RPC Nodes, or any other configuration for a Cosmos Node

## Guide 

* Step 1) Download [Akashlytics](https://akashlytics.com/deploy)
* Step 2) Copy and paste the deploy file below in the "Create Deployment" section of Akashlytics for a simple RPC node configuration

### Deploy File

Located in the main repo is are multiple deployment files to use on Akashlytics. Each deployment file is named after a simple node configuration. Here is the RPC config

```bash
---
version: "2.0"

services:
  node:
    image: chandrastation/akt-evmos:v3.0.2
    env:
      - MONIKER=akt_evmos
      - CHAIN_ID=evmos_9001-2
      - VALIDATE_GENESIS=0
      - P2P_PERSISTENT_PEERS=e3e11fca4ecf4035a751f3fea90e3a821e274487@bd-evmos-mainnet-seed-node-01.bdnodes.net:26656,fc86e7e75c5d2e4699535e1b1bec98ae55b16826@bd-evmos-mainnet-seed-node-02.bdnodes.net:26656,40f4fac63da8b1ce8f850b0fa0f79b2699d2ce72@seed.evmos.jerrychong.com:26656,eaa3dae2275faf9f599690c336d0e41e59fa6ae0@65.108.6.69:26656
      - GENESIS_URL=https://github.com/tharsis/mainnet/raw/main/evmos_9001-2/genesis.json.zip
      - SNAPSHOT_URL=https://snapshots.stakingcare.com/evmos/mainnet/evmos_2022-05-10.tar
      - SNAPSHOT_FORMAT=tar
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
          units: 8
        memory:
          size: 18Gi
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
* Step 3) Click through the deployment transactions, selecting a bid and submitting the manifest
* Step 4) Wait for the image to propogate and the node to sync

### Interaction
Connecting to the RPC or utilizing the Akash deployed node as a peer is as easy as adding the node id (printed in the logs or by clicking the URI and interacting with the RPC to visit the /status page and getting the node-id from there) and Akash URI to a typical node config.toml file under persistent peers. Further configuration can be found at the [Omni-Bus Repo](https://github.com/ovrclk/cosmos-omnibus)
