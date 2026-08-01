# 02 — OS Install & First Boot

## Flashing the OS

After backing up the existing contents of the USB stick, I flashed **Raspberry Pi OS (64-bit)** using Raspberry Pi Imager.

## First boot

First boot confirmed the OS installed correctly and the Pi 5 booted straight to the desktop:

![Welcome to Raspberry Pi Desktop](../assets/screenshots/01-first-boot-desktop.jpg)

## Verifying boot device

To confirm the system was actually booting from the USB stick (not falling back to any other storage), I checked block devices from the terminal:

```bash
lsblk
```

This confirmed the root filesystem was mounted from the USB drive as expected.

## Why this mattered later

Documenting this step turned out to be important — it's the baseline that later helped confirm *when* the USB drive started to develop problems (see the [incident writeup](03-incident-usb-failure-lessons-learned.md)).

Next: [Monitoring Service Setup →](../services/monitoring-stack/docs/01-docker-and-dashboards.md)
