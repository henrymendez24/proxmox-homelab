# Phase 3 – Initial OPNsense Setup

## Overview
This phase focused on the initial deployment and configuration of OPNsense inside my Proxmox homelab environment. The goal was to move from a basic virtual machine setup into a more realistic firewall and routing environment while preparing for future VLANs, segmentation, and remote management.

---

## Objectives
- Deploy OPNsense as a virtual firewall/router
- Configure WAN and LAN interfaces
- Create and assign Proxmox network bridges
- Establish management network access
- Test internet connectivity through double NAT
- Configure firewall access rules
- Integrate Tailscale for secure remote access
- Prepare the network for bridge mode deployment

---

## Technologies Used
- Proxmox VE
- OPNsense
- Tailscale
- Xfinity XB8 Gateway
- Linux Networking
- Virtual Bridges (vmbr0, vmbr1, vmbr2)

---

## Key Configuration Steps
1. Created virtual bridges inside Proxmox
2. Configured WAN and LAN interfaces in OPNsense
3. Verified internet connectivity through double NAT
4. Established Proxmox management networking
5. Added firewall rules for management access
6. Integrated Tailscale for remote administration
7. Tested interface assignments and routing
8. Prepared the environment for bridge mode migration

---

## Screenshots Included
The screenshots in this section document:
- Interface assignments
- Virtual bridge configuration
- Firewall rules
- Tailscale integration
- OPNsense dashboard setup
- Management network configuration
- Double NAT testing
- Bridge mode preparation

---

## Skills Demonstrated
- Firewall configuration
- Virtual networking
- Network troubleshooting
- Remote access configuration
- Linux networking concepts
- Proxmox virtualization
- Secure network design concepts

---

## Notes
This phase was an important milestone in building my homelab because it introduced a dedicated firewall and routing platform using OPNsense. It also provided hands-on experience with networking, virtualization, remote access, and troubleshooting in a real lab environment.
