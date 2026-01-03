# Grafana
Repository containing step-by-step installation and setup of Grafana on Ubuntu. Includes configuration files, service management, and best practices to deploy Grafana for monitoring, visualization, and observability.
# Grafana Installation and Log Monitoring Setup

This repository provides step-by-step instructions to install **Grafana** on Debian/Ubuntu and to set up **Loki** and **Promtail** using Docker for centralized log collection and visualization.

---

## Prerequisites

- Debian / Ubuntu system
- sudo privileges
- Internet access
- Docker (for Loki & Promtail)

---

## Install Grafana on Debian or Ubuntu

### Step 1: Install required packages
```bash
sudo apt update
sudo apt install -y apt-transport-https software-properties-common wget
