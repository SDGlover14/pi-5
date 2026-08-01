# Monitoring Stack (Netdata + Prometheus + Grafana)

Real-time system monitoring service running on the Pi 5 home server.

## Overview

**Goal:** surface real-time system health (CPU, memory, disk, temperature) via Grafana dashboards, backed by containerized services managed with Docker Compose.

## Documentation

1. **[Docker & Dashboard Setup](docs/01-docker-and-dashboards.md)** — installing Docker, first containers, `docker ps` verification
2. **[Monitoring: Netdata & Grafana](docs/02-monitoring-netdata-grafana.md)** — building out real-time dashboards, CPU/memory/temp/disk panels

For the initial hardware setup, OS install, and the USB boot-drive incident, see the [top-level docs](../../docs/).

## Stack

- Netdata (real-time metrics + dashboard)
- Prometheus (metrics scraping/storage, including scraping Netdata's Prometheus-format endpoint)
- Grafana (dashboarding on top of Prometheus)

## Screenshots

| | |
|---|---|
| ![docker ps](../../assets/screenshots/02-docker-ps-terminal.jpg) *Netdata container running via `docker ps`* | ![Grafana login](../../assets/screenshots/03-grafana-login-mobile.png) *Grafana login screen* |
| ![Hardware temp](../../assets/screenshots/04-grafana-hardware-temp.png) *Hardware temperature monitor* | ![CPU/Memory](../../assets/screenshots/05-grafana-cpu-memory.png) *CPU & memory dashboard* |
| ![Page faults](../../assets/screenshots/06-netdata-page-faults.png) *Netdata memory page faults* | |

## Deploy

```bash
cd services/monitoring-stack
docker compose up -d
```

- Netdata: `http://<pi-ip>:19999`
- Prometheus: `http://<pi-ip>:9090`
- Grafana: `http://<pi-ip>:3000`

---

[← Back to server overview](../../README.md)
