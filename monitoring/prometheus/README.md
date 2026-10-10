# Prometheus Infrastructure Monitoring

## Overview

Prometheus is used in my cybersecurity homelab to collect and query infrastructure monitoring metrics.

It runs as a Docker container on my Ubuntu Server 24.04 mini PC and provides a foundation for monitoring system and service performance.

## Technologies

- Ubuntu Server 24.04
- Docker
- Prometheus
- PromQL
- Grafana

## Architecture

The monitoring environment uses Prometheus as a metrics collection and query service, with Grafana providing dashboards and visualization.

**Monitoring workflow:**

1. Monitoring targets expose metrics.
2. Prometheus periodically scrapes configured targets.
3. Prometheus stores collected time-series data.
4. Grafana queries Prometheus to visualize metrics.

## Deployment

Prometheus was deployed using Docker on the Ubuntu server.

During setup, I worked with the Prometheus configuration file (`prometheus.yml`) to define monitoring targets and troubleshoot configuration issues.

## Useful Commands

### Check running containers

```bash
docker ps
```

### View Prometheus logs

```bash
docker logs <prometheus-container-name>
```

### Check container resource usage

```bash
docker stats
```

## Troubleshooting

During configuration, I encountered and investigated:

- Incorrect YAML formatting in `prometheus.yml`
- Empty or missing metrics
- Connectivity issues between monitoring services
- Grafana displaying a Bad Gateway error

These issues provided experience troubleshooting containerized monitoring services.

## Future Improvements

- Verify and document active scrape targets
- Add system-level metrics using Node Exporter
- Create Grafana dashboards for CPU, memory, disk, and network utilization
- Configure monitoring alerts for infrastructure issues

## Security Considerations

Credentials, tokens, and sensitive network details are excluded from this public documentation.
