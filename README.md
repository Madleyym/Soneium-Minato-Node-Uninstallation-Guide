# Soneium Minato Node Setup Guide

This README provides instructions for setting up and running a node for Soneium's public testnet "Minato".

Soneium is a layer-2 blockchain solution, and Minato is its public testnet. Running a node helps contribute to the network's decentralization and provides you with a direct interface to the blockchain.

## Hardware Requirements

We recommend the following minimum specifications:
- **Recommended AWS Instance**: i3.2xlarge or equivalent
- **CPU**: 8 cores
- **RAM**: 16 GB
- **Storage**: 100 GB SSD
- **Network**: 100 Mbps

For public RPC nodes, you will need to adjust resources based on your expected traffic.

## Prerequisites

Before setting up your Minato node, ensure you have:

- **Docker**: [Installation Guide](https://docs.docker.com/get-docker/)
- **Docker Compose**: [Installation Guide](https://docs.docker.com/compose/install/)
- **Ethereum RPC Node**: Access to an Ethereum RPC endpoint
- **Ethereum Beacon API**: Access to an Ethereum Beacon API endpoint

## Installation

### Docker Installation

1. **Create a directory for the node**:
   ```bash
   mkdir soneium-minato-node
   cd soneium-minato-node
   ```

2. **Download the configuration files**:
   - docker-compose.yml
   - minato-genesis.json
   - minato-rollup.json
   - sample.env

   These files are available from the official Soneium [documentation](https://docs.soneium.org/docs/builders/node/).

3. **Generate JWT Secret**:
   ```bash
   openssl rand -hex 32 > jwt.txt
   ```

4. **Configure Environment Variables**:
   ```bash
   mv sample.env .env
   ```
   
   Edit the `.env` file to set your Ethereum endpoints:
   ```
   L1_URL=<your_ethereum_rpc_node>
   L1_BEACON=<your_ethereum_beacon_api>
   ```

5. **Configure Public IP (If Behind NAT)**:
   
   If your node is behind a NAT device:
   
   - For op-geth, add to docker-compose.yml:
     ```
     --nat=extip:<your_node_public_ip>
     ```
   
   - For op-node, add to docker-compose.yml:
     ```
     --p2p.advertise.ip=<your_node_public_ip>
     ```

### Binary Installation

*Coming soon*: Instructions for setting up the node using binary files.

## Running the Node

Start the node using Docker Compose:

```bash
docker-compose up -d
```

## Monitoring

Monitor your node's logs:

For op-node-minato:
```bash
docker-compose logs -f op-node-minato
```

For op-geth-minato:
```bash
docker-compose logs -f op-geth-minato
```

## Troubleshooting

- **Sync Issues**: Ensure your L1 node is geographically close to the Minato node for faster synchronization
- **Connection Problems**: Verify firewall settings and network connectivity
- **Resource Limitations**: Check system resources if experiencing performance issues

## Additional Resources

- [Official Documentation](https://docs.soneium.org/docs/builders/node)
- [Soneium GitHub](https://github.com/soneium)
- [Community Discord](https://discord.gg/soneium)

---

This README is based on the official Soneium documentation. For the most up-to-date information, always refer to the [official documentation](https://docs.soneium.org/docs/builders/node).
```