# 05 — Incident: USB Drive Failure & Lessons Learned

## What happened

While troubleshooting the Prometheus scrape configuration (see [04](02-monitoring-netdata-grafana.md)), the USB stick being used as boot media began flashing its activity LED red — a hardware-level warning sign, not a software error message.

## Immediate response

Rather than continuing to troubleshoot through the desktop GUI (which generates ongoing disk I/O for window rendering, logging, etc.), I made the call to:

1. **Disable the GUI immediately** to cut down on unnecessary writes to the failing drive
2. **Switch to SSH** for all remaining configuration and troubleshooting
3. Complete the rest of the build headless, over SSH, until the stack was in a stable, working state

This prioritized protecting the data and the system's integrity over continuing the original troubleshooting task in the moment.

## Root cause

USB flash drives use flash memory not designed for the sustained, high-frequency write cycles that an OS, container runtime, and time-series metrics stack (Prometheus writing samples every few seconds) generate. Over time this wears out the flash cells, and the failure symptoms (a flashing red activity light, degraded read/write reliability) are consistent with a drive nearing end-of-life under that kind of load.

## The silver lining

This project was originally documented using a USB stick specifically because I wanted a spare drive to use for taking build screenshots and photos throughout the process — which meant I'd already backed up its original contents (family photos) to my laptop before flashing it. If the drive hadn't failed until *after* I'd stopped backing things up regularly, those photos could have been lost. The project inadvertently forced a backup that turned out to matter.

## What I'd do differently

| Then | Next time |
|---|---|
| USB flash drive as boot media | **SSD** (via USB 3.0 or NVMe HAT) — far better write endurance and sustained I/O performance |
| Noticed failure via GUI drive-activity LED | Set up **disk health monitoring** (e.g. `smartctl`/SMART where supported, or Netdata disk alerts) from the start, rather than relying on visual cues |
| Reactive switch to SSH mid-incident | Plan for **headless/SSH-only operation from day one** on any system running sustained workloads |

## Why this matters

Recognizing early warning signs on live infrastructure, making a fast decision to reduce risk (disable GUI, cut writes, move to SSH), and completing the task without losing data or progress — that's the kind of practical incident response judgment that applies directly to sysadmin/DevOps work, not just homelab tinkering.

---

[← Back to project overview](../README.md)
