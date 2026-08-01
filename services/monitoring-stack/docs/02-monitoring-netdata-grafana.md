# 04 — Monitoring: Netdata & Grafana

## Standing up Grafana

With Netdata collecting metrics, the next step was a proper dashboarding layer. I deployed Grafana alongside the existing stack and logged in via its web UI:

![Welcome to Grafana](../../../assets/screenshots/03-grafana-login-mobile.png)

## Building dashboards

Using Grafana's Node Exporter dashboard templates, I built out panels covering:

- **Hardware temperature monitoring** — CPU thermal zones and the RP1 I/O controller sensor, tracked over time with min/mean/max
- **CPU utilization** — busy system/user/iowait/idle breakdown
- **Memory usage** — total/used/cache+buffer/free/swap
- **Disk space** — usage by mount point
- **Network traffic** — RX/TX by interface

![Hardware temperature dashboard](../../../assets/screenshots/04-grafana-hardware-temp.png)
![CPU and memory dashboard](../../../assets/screenshots/05-grafana-cpu-memory.png)

## The Prometheus sticking point

Getting Prometheus configured to scrape and feed metrics into Grafana correctly took longer than expected — this was the point in the build where I was actively debugging metric exporters and scrape configs when the [USB drive incident](03-incident-usb-failure-lessons-learned.md) occurred.

Netdata's own dashboard was useful here as a sanity check while troubleshooting — comparing its live memory/page-fault graphs against what Prometheus/Grafana were reporting helped isolate where the data pipeline was breaking:

![Netdata memory page faults](../../../assets/screenshots/06-netdata-page-faults.png)

Next: [Incident: USB Drive Failure & Lessons Learned →](03-incident-usb-failure-lessons-learned.md)
