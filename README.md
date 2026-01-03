
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

Step 2: Add Grafana GPG key
sudo mkdir -p /etc/apt/keyrings
wget -q -O - https://apt.grafana.com/gpg.key | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null

Step 3: Add Grafana repository

Choose only ONE repository (Stable is recommended)

Stable Release (Recommended)
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" \
| sudo tee /etc/apt/sources.list.d/grafana.list

Beta Release (Optional)
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com beta main" \
| sudo tee /etc/apt/sources.list.d/grafana.list

Step 4: Install Grafana
sudo apt update
sudo apt install -y grafana

Step 5: Start and enable Grafana service
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
sudo systemctl status grafana-server


Grafana will be available at:

http://<server-ip>:3000


Default credentials:

admin / admin

Install Loki and Promtail using Docker
Step 1: Install Docker

Follow official Docker installation:
https://docs.docker.com/engine/install/

Verify Docker:

docker --version

Step 2: Download Loki configuration
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml \
-O loki-config.yaml

Step 3: Download Promtail configuration
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml \
-O promtail-config.yaml

Step 4: Run Loki container
docker run -d \
  --name loki \
  -p 3100:3100 \
  -v $(pwd)/loki-config.yaml:/etc/loki/loki-config.yaml \
  grafana/loki:2.8.0 \
  --config.file=/etc/loki/loki-config.yaml

Step 5: Run Promtail container
docker run -d \
  --name promtail \
  -v $(pwd)/promtail-config.yaml:/etc/promtail/promtail-config.yaml \
  -v /var/log:/var/log \
  --network host \
  grafana/promtail:2.8.0 \
  --config.file=/etc/promtail/promtail-config.yaml


Note: Ensure Promtail is configured to send logs to http://localhost:3100.

Verify Setup
Check running containers
docker ps

Check Loki API
curl http://localhost:3100/ready

Grafana Data Sources

After login, add:

Prometheus (if installed): http://localhost:9090

Loki: http://localhost:3100

Directory Structure (Suggested)
grafana_configs/
├── README.md
├── loki-config.yaml
└── promtail-config.yaml

Summary

Grafana for visualization

Loki for log aggregation

Promtail for log shipping

Docker-based log pipeline

Suitable for learning and small monitoring setups

Next Improvements

Use Docker Compose

Enable HTTPS for Grafana

Add Prometheus metrics

Create dashboards and alerts

License

MIT License


---

If you want, I can also:
- Convert this to **Docker Compose**
- Add **Prometheus + dashboards**
- Make it **production-ready**
- Simplify for **beginners**

Just tell me.
