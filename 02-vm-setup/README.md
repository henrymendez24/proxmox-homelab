# OPNsense VM Setup in Proxmox

## Objective
This lab simulates deploying a virtual firewall/router in a homelab environment by creating and installing an OPNsense virtual machine in Proxmox.

**Topology (high-level):**
Proxmox → vmbr1 (WAN to ISP/router)  
Proxmox → vmbr0 (LAN to internal network)

## ISO Upload

The OPNsense ISO was uploaded to Proxmox storage and verified.

![ISO Upload](screenshots/iso-upload-success.png)

## Virtual Machine Creation

### General
- VM Name: OPNsense
- Guest OS Type: Other

![General](screenshots/vm-creation-general.png)

### System
- BIOS: OVMF (UEFI)
- Machine Type: q35
- EFI Disk enabled

![System](screenshots/vm-creation-system.png)

### Disks
- Storage: local-lvm
- Disk size: 32GB
- Bus/Device: VirtIO

![Disks](screenshots/vm-creation-disks.png)

### CPU
- 2 cores assigned

![CPU](screenshots/vm-creation-cpu.png)

### Memory
- 4GB RAM allocated

![Memory](screenshots/vm-creation-memory.png)

### Network
- Adapter Model: VirtIO (paravirtualized)
- Interfaces:
  - net0 → vmbr0 (LAN)
  - net1 → vmbr1 (WAN)

![Network](screenshots/vm-creation-network.png)

## Boot Issues & Fix

Initial boot failed due to incorrect boot order.

### Before

![Boot Order Before](screenshots/boot-order-before.png)

### After

![Boot Order After WAN](screenshots/boot-order-after-wan.png)

### WAN Interface Verification

![WAN Interface](screenshots/network-wan-vmbr1.png)

### Fix:
- Moved CD-ROM (ISO) above disk to start the installer
- Verified disk and NIC order before reboot

## OPNsense Installation Process
This section documents the full installation workflow of OPNsense within a Proxmox virtual machine.

Installation steps:

- Selected default keymap
- Chose guided installation
- Selected target disk (32GB virtual disk)
- Confirmed partitioning
- Set root password
- Completed installation and rebooted

### Installation Screens

#### Keymap

![Keymap](screenshots/opnsense-install-keymap.png)

#### Installer Menu

![Installer Menu](screenshots/opnsense-install-menu.png)

#### Disk Selection

![Disk Selection](screenshots/opnsense-install-disk-selection.png)

#### Swap

![Swap](screenshots/opnsense-install-swap.png)

#### Confirm Disk

![Confirm Disk](screenshots/opnsense-install-confirm-disk.png)

#### Install Progress

![Progress](screenshots/opnsense-install-progress.png)

#### Set Password

![Set Password](screenshots/opnsense-install-set-password.png)

#### Install Complete

![Install Complete](screenshots/opnsense-install-complete.png)

#### Reboot

![Reboot](screenshots/opnsense-install-reboot.png)

## Post-Install Console Output
Access the web UI at https://192.168.1.1 (self-signed certificate).

Validated connectivity from LAN (ping 8.8.8.8 and DNS resolution) after WAN obtained a DHCP lease.

After installation, OPNsense displayed:

- LAN interface: 192.168.1.1/24
- WAN interface: DHCP assigned (10.0.0.x)

The system successfully booted into the OPNsense environment.

![Console Output](screenshots/opnsense-post-install-console.png)

## Key Takeaways

- Confirmed internet access from LAN after install (via WAN DHCP)
- VirtIO was used for better performance in Proxmox
- Separate WAN bridge (vmbr1) was created later for proper network separation
- Identified and resolved a boot order misconfiguration during VM deployment
- Verified WAN connectivity via DHCP assignment after initial boot

## Next Step

Proceed to initial OPNsense configuration (next phase of the lab):
- Interface assignment
- WAN/LAN setup
- Connectivity testing

## Follow-up
See: [OPNsense Initial Configuration](screenshots/../opnsense-initial-configuration/README.md)
