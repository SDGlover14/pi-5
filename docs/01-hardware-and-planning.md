# 01 — Hardware & Planning

## The kit

- **Raspberry Pi 5 (16GB)** — chosen as the primary server for its performance headroom (enough RAM and CPU to comfortably run Docker + multiple monitoring containers without swapping).
- **Raspberry Pi Zero 2 WH** and **Raspberry Pi 1B** — earmarked for future homelab expansion (e.g. remote monitoring nodes, low-power services).

## Boot media decision

Every guide recommends a microSD card or SSD for boot media. I didn't have a spare SD card large enough on hand, but I did have a USB memory stick.

Before repurposing it, I backed up the personal photos stored on it to my laptop — a routine precaution, but one that turned out to matter more than expected (see the [incident writeup](03-incident-usb-failure-lessons-learned.md)).

**Decision at the time:** use the USB stick as boot media, planning to document the whole build from first boot through to a working monitoring stack.

## Plan

1. Flash Raspberry Pi OS (64-bit) to the USB stick
2. Boot the Pi 5 from USB and confirm via `lsblk`
3. Install Docker
4. Deploy Netdata for real-time system metrics
5. Deploy Grafana + Prometheus for dashboarding
6. Document each stage with terminal screenshots

Next: [OS Install & First Boot →](02-os-install-and-first-boot.md)
