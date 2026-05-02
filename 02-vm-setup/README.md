# OPNsense VM Setup in Proxmox

## Objective
Create and install an OPNsense virtual machine in Proxmox to serve as a firewall/router.

---

## ISO Upload
The OPNsense ISO was uploaded to Proxmox storage and verified.

---

## Virtual Machine Creation

### General
- VM Name: OPNsense
- Guest OS Type: Other

### System
- BIOS: OVMF (UEFI)
- Machine Type: q35
- EFI Disk enabled

### Disks
- Storage: local-lvm
- Disk size: 32GB
- Bus/Device: VirtIO

### CPU
- 2 cores assigned

### Memory
- 4GB RAM allocated

### Network
- Adapter Model: VirtIO (paravirtualized)
- Added 2 interfaces:
  - net0 → vmbr0 (LAN initially)
  - net1 → vmbr1 (WAN bridge added later)

---

## Boot Issues & Fix

Initial boot failed due to incorrect boot order.

### Fix:
- Adjusted boot order to prioritize ISO (cdrom)
- Ensured disk and network devices were correctly ordered

---

## OPNsense Installation Process

Steps completed during installation:

- Selected default keymap
- Chose guided installation
- Selected target disk (32GB virtual disk)
- Confirmed partitioning
- Set root password
- Completed installation and rebooted

---

## Post-Install Console Output

After installation, OPNsense displayed:

- LAN interface: 192.168.1.1/24
- WAN interface: DHCP assigned (10.0.0.x)

System successfully booted into OPNsense environment.

---

## Screenshots

### ISO Upload
![ISO Upload](screenshots/vm-config.png)

### VM Creation
![VM Creation](screenshots/interface-setup.png)

### Boot Menu
![Boot Menu](screenshots/arp-test.png)

---

## Notes

- VirtIO was used for better performance in Proxmox
- Separate WAN bridge (vmbr1) was created later for proper network separation
- Boot order misconfiguration is a common issue when installing VMs

---

## Next Step

Proceed to initial OPNsense configuration:
- Interface assignment
- WAN/LAN setup
- Connectivity testing