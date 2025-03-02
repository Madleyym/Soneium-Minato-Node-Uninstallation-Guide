# Soneium Minato Node Uninstallation Guide

## About This Document
This document contains instructions on how to uninstall a node for Soneium's public testnet Minato. This guide is based on experience running a node following the official documentation from [Soneium Documentation](https://docs.soneium.org/docs/builders/node).

## Node Uninstallation Steps

### 1. Stop and Remove Containers
Make sure you are in the node installation directory:
```bash
cd soneium-minato-node
```

Stop and remove containers:
```bash
docker-compose down
```

### 2. Remove Data Volumes (Optional)
To remove all node data:
```bash
docker-compose down -v
```

### 3. Remove Docker Images (Optional)
```bash
docker rmi $(docker images | grep "op-geth\|op-node" | awk '{print $3}')
```

### 4. Remove Node Directory (Optional)
```bash
cd ..
rm -rf soneium-minato-node
```

### 5. Verify Uninstallation
Ensure all containers have been removed:
```bash
docker ps -a | grep minato
```

Ensure all volumes have been removed (if using the `-v` option):
```bash
docker volume ls | grep minato
```

---

**Note:** This document was created based on experience running a Soneium Minato node following the official documentation. For the latest information, always refer to the [official Soneium documentation](https://docs.soneium.org/docs/builders/node).

Last updated: 2025-03-02 14:23:20
Prepared by: Madleyym