
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

Step 2: Add Grafana GPG key
sudo mkdir -p /etc/apt/keyrings
wget -q -O - https://apt.grafana.com/gpg.key | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null

Step 3: Download Promtail configuration
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml \
-O promtail-config.yaml
