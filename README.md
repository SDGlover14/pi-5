# Pi 5 Home Server

> A general-purpose home server built on a Raspberry Pi 5, running containerized services managed with Docker. Part of a wider three-device homelab used to build practical Linux administration, containerization, and DevOps skills — aimed at moving from IT Helpdesk into a Junior DevOps / Systems Administrator role.

![Raspberry Pi](https://img.shields.io/badge/Raspberry%20Pi-5-c51a4a?logo=raspberrypi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black)
![Status](https://img.shields.io/badge/status-active-brightgreen)

---

## Overview

The Pi 5 (16GB) is the main server in a three-device Raspberry Pi homelab. Rather than a single-purpose box, it's set up to run multiple containerized services side by side — each one documented as its own scoped project under `services/`.

**Other devices in the homelab** (each with their own dedicated repo — see [my profile](https://github.com/YOUR-USERNAME)):

| Device | Role |
|---|---|
| Raspberry Pi Zero 2 WH | Print server + VPN gateway |
| Raspberry Pi 1B | Dedicated Pi-hole DNS/ad-blocking |

Pi-hole could run as a container on this Pi 5 instead, but it's deliberately kept on its own dedicated Pi 1B — isolating DNS/ad-blocking from this server and preserving the Pi 5's resources for the services below.

## Services running on this server

| Service | Description |
|---|---|
| [monitoring-stack](services/monitoring-stack/) | Netdata + Prometheus + Grafana — real-time system metrics and dashboards |

*(more services added here as the server grows — reverse proxy, media server, file storage, etc.)*

## Build & Setup Documentation

General server setup — read in order:

1. **[Hardware & Planning](docs/01-hardware-and-planning.md)** — kit, boot media decision, initial setup
2. **[OS Install & First Boot](docs/02-os-install-and-first-boot.md)** — flashing Raspberry Pi OS, verifying boot via `lsblk`
3. **[Incident: USB Drive Failure & Lessons Learned](docs/03-incident-usb-failure-lessons-learned.md)** — what went wrong, how I recovered, what I'd do differently

Per-service setup and screenshots live inside each service's own folder — e.g. [services/monitoring-stack/](services/monitoring-stack/).

## Stack

- **OS:** Raspberry Pi OS (64-bit)
- **Container runtime:** Docker + Docker Compose
- **Access:** SSH-managed (headless) after initial setup

## Key Skills Demonstrated

- Linux system administration (headless/SSH-only operation)
- Docker & Docker Compose container orchestration
- Monitoring/observability tooling (Netdata, Prometheus, Grafana)
- Incident response under a live build (diagnosing and reacting to failing storage media)
- Deliberate infrastructure design decisions (dedicated hardware vs. containerization tradeoffs)
- Technical documentation and root-cause reflection

## Lessons Learned (short version)

Mid-build, the USB stick used as boot media began to fail (visible as a flashing red drive-activity LED) while troubleshooting the monitoring stack. I immediately disabled the GUI and completed the remaining configuration over SSH to avoid further disk writes, then migrated off the failing media.

**Takeaway:** USB flash drives are not reliable long-term boot media. Next build uses an SSD over USB 3.0 (or NVMe HAT) for boot storage. Full writeup in [docs/03](docs/03-incident-usb-failure-lessons-learned.md).

## Next Steps

- [ ] Migrate boot media to SSD
- [ ] Add a reverse proxy service
- [ ] Expand services as the server takes on more workloads
- [ ] Add alerting (Grafana Alerting / Prometheus Alertmanager)
- [ ] Automate provisioning with Ansible

---

*Part of my ongoing homelab series — see my [profile README](https://github.com/SDGlover14) for the full list of projects.*
