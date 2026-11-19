# Phase 6 – Docker Services (Raspberry Pi 5)

## Overview
A Raspberry Pi 5 runs the lab's supporting services as Docker containers, managed through Portainer. Running them on the Pi keeps monitoring and management tools separate from the Proxmox host they watch.

## Host

| Component | Details |
|---|---|
| Device | Raspberry Pi 5, 8 GB |
| Storage | 512 GB NVMe SSD on an NVMe HAT |
| Network | Wired gigabit Ethernet |
| Remote access | Tailscale |

## Services

| Service | Purpose in the lab |
|---|---|
| Portainer | Web interface for managing containers, images and volumes |
| Nginx Proxy Manager | Reverse proxy for the lab's internal web interfaces |
| Grafana | Dashboards for lab metrics |
| Uptime Kuma | Uptime monitoring and alerts for lab services |
| Netdata | Real-time CPU, memory, disk and network metrics |
| Omada Controller | Manages the TP-Link Omada Wi-Fi access point |
| Cowrie | SSH/Telnet honeypot that logs attacker activity |

## Status
🟡 Documentation in progress.

- [ ] Screenshot of each service's dashboard
- [ ] `docker-compose.yml` with passwords and secrets removed
- [ ] Notes on container networking and how each service is reached
