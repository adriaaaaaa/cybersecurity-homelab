# Cybersecurity Homelab Architecture

## Overview

This document illustrates the logical architecture of my cybersecurity homelab.

The environment consists of a dedicated Ubuntu Server mini PC hosting containerized infrastructure monitoring and security services, with Wazuh agents installed on both Ubuntu and Windows.

## Architecture Diagram

```mermaid
flowchart TB
    W["Windows Desktop<br/>Wazuh Agent"]
    U["Ubuntu Server 24.04<br/>Wazuh Agent"]

    subgraph H["Ubuntu Mini PC — Docker"]
        M["Wazuh Manager"]
        I["Wazuh Indexer"]
        D["Wazuh Dashboard"]
        P["Prometheus"]
        G["Grafana"]
    end

    W -->|"Security events"| M
    U -->|"Security events"| M
    M --> I
    I --> D
    P -->|"Metrics"| G

    classDef endpoint fill:#dbeafe,stroke:#2563eb,color:#1e3a8a
    classDef security fill:#dcfce7,stroke:#16a34a,color:#14532d
    classDef monitoring fill:#fef3c7,stroke:#d97706,color:#78350f

    class W,U endpoint
    class M,I,D security
    class P,G monitoring
```

## Infrastructure Components

### Ubuntu Server

The Ubuntu mini PC provides the underlying infrastructure, hosting Docker containers and the local Wazuh agent.

### Wazuh SIEM

Wazuh provides centralized security event collection, analysis, storage, and visualization for Linux and Windows endpoints.

### Prometheus and Grafana

Prometheus provides metrics collection and querying, while Grafana provides infrastructure monitoring visualizations.

## Future Improvements

- Add verified network and service communication details.
- Document active Prometheus scrape targets.
- Expand the architecture as additional security tools are deployed.
