# Cybersecurity Homelab

## Overview

This project documents my personal cybersecurity and infrastructure homelab, built to develop hands-on experience with Linux administration, networking, containerization, system monitoring, and security operations.

The homelab runs on a dedicated PC using Ubuntu Server 24.04. It hosts containerized monitoring and security tools, including Prometheus, Grafana, and Wazuh SIEM.

The goal is to build a practical environment for monitoring systems, investigating security events, troubleshooting infrastructure, and developing security skills.

## Technologies Used

| Category | Technologies |
|---|---|
| Operating System | Ubuntu Server 24.04, Windows |
| Containerization | Docker, Docker Compose |
| Infrastructure Monitoring | Prometheus |
| Visualization | Grafana |
| Security Monitoring | Wazuh SIEM 4.14.8 |
| Networking | TCP/IP, SSH, Linux networking |
| Security Analysis | Windows Event Logs, Wazuh Threat Hunting |

## Project Components

### 1. Ubuntu Server Infrastructure
- Configured a dedicated Ubuntu Server homelab.
- Enabled SSH for remote administration.
- Configured networking for access from other devices.
- Installed Docker to host containerized services.

### 2. Infrastructure Monitoring
- Deployed Prometheus for collecting system metrics.
- Configured Grafana for monitoring and visualization.
- Troubleshot monitoring service connectivity and configuration.

### 3. Wazuh SIEM Deployment
- Deployed Wazuh Manager, Indexer, and Dashboard using Docker Compose.
- Configured centralized security monitoring.
- Installed Wazuh agents on Ubuntu and Windows.
- Verified endpoint connectivity and security alert collection.

### 4. Security Investigations
**Lab 01: Windows Failed Login Detection**
- Generated a controlled Windows authentication failure.
- Identified Windows Security Event ID 4625.
- Located the corresponding alert in Wazuh.
- Analyzed the detection rule, severity, logon type, and authentication status.

## Repository Structure

## Project Documentation

| Component | Description | Documentation |
|---|---|---|
| Architecture | Homelab infrastructure and service communication | [View Architecture](architecture/README.md) |
| Ubuntu Server | Linux server setup and administration | [View Documentation](ubuntu-server/README.md) |
| Docker | Container deployment and management | [View Documentation](docker/README.md) |
| Prometheus | Infrastructure metrics collection | [View Documentation](monitoring/prometheus/README.md) |
| Grafana | Monitoring dashboards and visualization | [View Documentation](monitoring/grafana/README.md) |
| Wazuh SIEM | Security monitoring and endpoint management | [View Documentation](security/wazuh/README.md) |

## Security Investigations

| Lab | Description | Documentation |
|---|---|---|
| Lab 01 | Windows Failed Login Detection (Event ID 4625) | [View Investigation](security/wazuh/investigations/windows-failed-login.md) |

Additional security labs will be documented as the homelab expands.

## Project Goals

- Develop practical Linux and network administration skills.
- Gain experience deploying and maintaining security tools.
- Understand centralized logging and security event analysis.
- Practice investigating authentication failures and suspicious activity.
- Expand the homelab with additional security detection exercises.

## Project Status

**Active — Ongoing Development**

This repository will be updated as new security labs, monitoring capabilities, and infrastructure improvements are completed.
