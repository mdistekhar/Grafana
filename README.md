
# Grafana Installation and Log Monitoring Setup

This repository provides step-by-step instructions to install **Grafana** on Debian/Ubuntu and to set up **Loki** and **Promtail** using Docker for centralized log collection and visualization.


---

## Prerequisites

- Debian / Ubuntu system
- sudo privileges
- Internet access
- Docker (for Loki & Promtail)

---




# 📄 Grafana, Loki & Promtail Installation Guide (Ubuntu/Debian)

---

## 🔹 Install Grafana on Debian/Ubuntu

### 1. Install Required Packages

```bash
sudo apt-get install -y apt-transport-https software-properties-common wget
```

---

### 2. Add Grafana GPG Key

```bash
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key
```

---

### 3. Add Grafana Repository

#### Stable Release (Recommended)

```bash
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
```

#### Beta Release (Optional)

```bash
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com beta main" | sudo tee /etc/apt/sources.list.d/grafana.list
```

---

### 4. Update Packages

```bash
sudo apt-get update
```

---

### 5. Install Grafana

```bash
sudo apt-get install grafana
```

---

### 6. Start and Enable Grafana

```bash
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
sudo systemctl status grafana-server
```

---

### 7. Access Grafana

Open in browser:

```
http://localhost:3000
```

**Default Login:**

* Username: admin
* Password: admin

---

## 🔹 Install Loki and Promtail using Docker

### 1. Download Loki Configuration

```bash
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
```

---

### 2. Download Promtail Configuration

```bash
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml
```

---

### 3. Run Loki Container

```bash
docker run -d --name loki \
-v $(pwd):/mnt/config \
-p 3100:3100 \
grafana/loki:2.8.0 \
--config.file=/mnt/config/loki-config.yaml
```

---

### 4. Run Promtail Container

```bash
docker run -d --name promtail \
-v $(pwd):/mnt/config \
-v /var/log:/var/log \
--link loki \
grafana/promtail:2.8.0 \
--config.file=/mnt/config/promtail-config.yaml
```

---

## 🔹 Summary

This setup provides:

* 📊 Monitoring using Grafana
* 📈 Metrics visualization
* 📜 Log collection using Promtail
* 📦 Log storage using Loki

---

## 🔹 Best Practices

* Always run commands in a **single line**
* Verify services using `systemctl status`
* Ensure ports (3000, 3100) are open
* Use Docker for quick and clean setup

---

## 🔹 Conclusion

This configuration creates a **complete observability stack** using Grafana, Loki, and Promtail, enabling real-time monitoring and log analysis in a Linux environment.

---
