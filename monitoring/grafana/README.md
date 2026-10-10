# Grafana Monitoring Dashboard

## Overview

Grafana is used in my cybersecurity homelab to visualize infrastructure metrics collected by Prometheus.

Grafana runs in a Docker container on my Ubuntu Server 24.04 mini PC, alongside other monitoring and security services.

## Technologies Used

- Ubuntu Server 24.04
- Docker
- Grafana
- Prometheus
- PromQL

## Monitoring Architecture

The monitoring stack follows this workflow:

**Monitoring Targets → Prometheus → Grafana**

Prometheus collects and stores time-series metrics, while Grafana queries those metrics and displays them through dashboards.

## Deployment

Grafana was deployed using Docker on the Ubuntu server.

The setup involved:

- Running Grafana as a containerized service
- Accessing the Grafana web interface
- Working with Prometheus as a monitoring data source
- Troubleshooting connectivity and service availability

## Useful Docker Commands

### Check Grafana container status

```bash
docker ps
```

### View Grafana logs

```bash
docker logs <grafana-container-name>
```

### Check container resource usage

```bash
docker stats
```

## Troubleshooting Experience

During the initial setup, I investigated several issues:

- Grafana displaying a Bad Gateway error
- Connection timeouts between monitoring services
- Prometheus returning empty metrics
- Prometheus YAML configuration errors

These issues provided practical experience with Docker networking, service connectivity, and infrastructure monitoring.

## Planned Improvements

- Verify Prometheus data source connectivity
- Build CPU, memory, disk, and network monitoring dashboards
- Configure infrastructure alerting
- Add screenshots of monitoring dashboards
- Document custom PromQL queries

## Security Considerations

Dashboard screenshots and configuration examples will be reviewed to ensure passwords, authentication tokens, and sensitive system information are not exposed.
