# 03 — Docker & Dashboard Setup

## Installing Docker

With the OS confirmed booting correctly, I installed Docker on the Pi 5 to run the monitoring stack in containers rather than installing everything directly on the host — keeping the system clean and each service isolated and reproducible.

## First container: Netdata

Netdata was the first service deployed, run via a `docker-compose.yml` in a dedicated `~/netdata` directory:

```bash
cd ~/netdata
ls
# docker-compose.yml

docker compose up -d
```

Compose pulled the image, created the network, and brought up the volumes and container:

- Image `netdata/netdata:stable` pulled
- Network `netdata_default` created
- Volumes `netdata-cache`, `netdata-config`, `netdata-lib` created
- Container `netdata` started

## Verifying the container

```bash
docker ps
```

```
CONTAINER ID   IMAGE                    COMMAND            CREATED         STATUS                   PORTS
97e0efb47204   netdata/netdata:stable   "/usr/sbin/run.sh"  6 minutes ago   Up 6 minutes (healthy)  0.0.0.0:19999->19999/tcp
```

![docker ps output](../../../assets/screenshots/02-docker-ps-terminal.jpg)

## Confirming network reachability

```bash
hostname -I
# 192.168.1.20 ...
```

With the container healthy and the host IP confirmed, the Netdata dashboard was reachable at `http://192.168.1.20:19999` from other devices on the network.

Next: [Monitoring with Netdata & Grafana →](02-monitoring-netdata-grafana.md)
