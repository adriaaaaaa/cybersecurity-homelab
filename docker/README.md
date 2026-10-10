# Docker Infrastructure

## Overview

Docker is used to deploy and manage containerized applications in my Ubuntu Server cybersecurity homelab.

Containerization allows multiple monitoring and security services to run on the same physical server while maintaining separate application environments.

## Environment

- **Host Operating System:** Ubuntu Server 24.04
- **Container Platform:** Docker Engine
- **Multi-Container Management:** Docker Compose
- **Hardware:** Dedicated mini PC

## Containerized Services

| Service | Purpose |
|---|---|
| Prometheus | Collects infrastructure monitoring metrics |
| Grafana | Visualizes monitoring data |
| Wazuh Manager | Processes endpoint security events |
| Wazuh Indexer | Stores and indexes security data |
| Wazuh Dashboard | Provides security monitoring and investigation interfaces |

## Docker Administration

Useful commands for managing the homelab:

### View running containers

```bash
docker ps
```

### View all containers

```bash
docker ps -a
```

### View container logs

```bash
docker logs <container-name>
```

### Check resource utilization

```bash
docker stats
```

### View Docker Compose services

From a directory containing a Compose configuration:

```bash
docker compose ps
```

## Wazuh Docker Deployment

Wazuh was deployed using a single-node Docker Compose configuration containing three primary services:

1. Wazuh Manager
2. Wazuh Indexer
3. Wazuh Dashboard

The Wazuh Manager receives security events from agents installed on the Ubuntu server and Windows desktop.

The Indexer stores searchable security data, while the Dashboard provides an interface for investigating alerts.

## Troubleshooting Experience

During deployment, I worked through:

- Container connectivity and service availability
- Wazuh Dashboard authentication issues
- API credential configuration
- Container service health checks
- Security event collection and verification

## Security Considerations

Sensitive configuration files, passwords, private keys, certificates, and authentication tokens are excluded from the public repository.

Configuration examples will be sanitized before publication.
