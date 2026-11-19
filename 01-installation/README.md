# Phase 1 – Proxmox Installation

## Overview
Proxmox VE was installed on a dedicated physical machine to serve as the base for my homelab. The host runs the OPNsense firewall (VM 101) and the Windows Server 2025 domain controller (VM 100).

## Hardware

| Component | Details |
|---|---|
| CPU | AMD Ryzen 7 3700X (8 cores / 16 threads) |
| RAM | 32 GB Corsair DDR4-3600 |
| Storage | 1 TB SSD |
| Network | Intel NIC (WAN), Realtek NIC (LAN / VLAN trunk), USB NIC (out-of-band management) |
| Hypervisor | Proxmox VE 9 |

## Steps
- Downloaded the Proxmox ISO
- Created a bootable USB
- Installed Proxmox on bare metal
- Accessed the web interface at `https://<ip>:8006`

## Notes
The installation was straightforward with no issues encountered. Network bridges and the OPNsense VM are covered in [Phase 2](../02-vm-setup/) and [Phase 3](../03-opnsense-deployment/).
