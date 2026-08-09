# Phase 4 – Security Hardening

---

## Overview

This phase focused on hardening the homelab environment across four areas: OPNsense intrusion detection and prevention, Proxmox host security, network segmentation using VLANs, and certificate management. The goal was to move from a functional but default-configured lab into a more secure and production-realistic environment.

---

## Objectives

- Enable and tune Suricata IDS/IPS on OPNsense for threat detection
- Harden the Proxmox host (disable root SSH, enable 2FA, configure datacenter firewall)
- Design and implement VLAN segmentation (Trusted, IoT, Management, DMZ)
- Replace self-signed certificates with trusted certs via Let's Encrypt or an internal CA

---

## Technologies Used

- Proxmox VE
- OPNsense
- Suricata (IDS/IPS)
- Let's Encrypt / ACME
- OpenSSL (internal CA)
- Linux Networking
- Virtual Bridges (vmbr0, vmbr1, vmbr2)
- Google Authenticator / TOTP (Proxmox 2FA)

---

## Phase Breakdown

### Phase 4.1 – OPNsense IDS/IPS (Suricata)

**Key Configuration Steps**

1. Install the Suricata plugin via OPNsense package manager
2. Enable Suricata on the WAN interface
3. Download and activate Emerging Threats Open ruleset
4. Set interface to IPS mode (inline) to block, not just alert
5. Configure alert logging and review the live log
6. Tune false positives by suppressing noisy rules
7. Validate IPS is blocking test traffic

**Screenshots Included**

The screenshots in this section document:

- Suricata plugin installation
- Interface configuration (WAN, IPS mode)
- Ruleset download and activation
- Live alert log
- IPS block confirmation

---

### Phase 4.2 – Proxmox Host Hardening

**Key Configuration Steps**

1. Disable root SSH login (`PermitRootLogin no` in `/etc/ssh/sshd_config`)
2. Create a non-root admin user with `sudo` privileges
3. Enable two-factor authentication (TOTP) on the Proxmox web UI
4. Configure the Proxmox datacenter firewall with default DROP policy
5. Add explicit ACCEPT rules for management access (SSH, web UI)
6. Disable the Proxmox subscription nag (optional)
7. Review and restrict API token permissions

**Screenshots Included**

The screenshots in this section document:

- SSH hardening config
- Proxmox 2FA setup (TOTP enrollment)
- Datacenter firewall rules
- Non-root user creation and permissions

---

### Phase 4.3 – Network Segmentation / VLANs

**Key Configuration Steps**

1. Define VLAN strategy and IP schema:
   - MGMT – Management (192.168.99.0/24, opt1/vtnet2 — untagged, not a VLAN)
   - VLAN 10 – Trusted (192.168.10.0/24)
   - VLAN 20 – Servers (192.168.20.0/24)
   - VLAN 30 – IoT (192.168.30.0/24)
   - VLAN 40 – Lab (192.168.40.0/24)
2. Enable VLAN-aware bridging on the Proxmox bridge
3. Create VLAN interfaces in OPNsense (Interfaces → Other Types → VLAN)
4. Assign and enable each VLAN interface in OPNsense
5. Configure DHCP server for each VLAN
6. Set inter-VLAN firewall rules (default deny between segments)
7. Add selective allow rules (e.g. Trusted → MGMT for admin access, block IoT → Trusted)
8. Test segmentation with cross-VLAN ping tests

**Screenshots Included**

The screenshots in this section document:

- VLAN interface creation in OPNsense
- DHCP scope configuration per VLAN
- Inter-VLAN firewall rules
- Proxmox VLAN-aware bridge config
- Segmentation test results

---

### Phase 4.4 – Certificate Management

**Key Configuration Steps**

1. Choose certificate strategy (Let's Encrypt for public domain OR internal CA for LAN-only)
2. **Let's Encrypt path:** Install ACME plugin in OPNsense, configure DNS challenge, issue cert for OPNsense web UI
3. **Internal CA path:** Create a root CA with OpenSSL, import into OPNsense as a trusted CA
4. Issue and install a certificate for the OPNsense web UI
5. Issue and install a certificate for the Proxmox web UI
6. Import the CA cert into browser/OS trust store on admin machines
7. Verify HTTPS access with no browser warnings on both UIs

**Screenshots Included**

The screenshots in this section document:

- ACME plugin setup (Let's Encrypt path)
- Internal CA creation (OpenSSL path)
- Certificate assignment on OPNsense
- Certificate assignment on Proxmox
- Browser showing valid HTTPS with no warnings

---

## Skills Demonstrated

- Intrusion detection and prevention (IDS/IPS)
- Host hardening and least-privilege access
- Multi-factor authentication
- VLAN design and implementation
- Firewall rule logic and network segmentation
- Certificate authority management
- TLS/HTTPS configuration

---

## Notes

This phase transformed the homelab from a functional default setup into a hardened, segmented environment closer to real-world network architecture. Each sub-phase builds on the previous one — segmentation is most effective once the firewall (IDS/IPS) and host access (Proxmox hardening) are locked down first. Certificate management is done last so valid HTTPS is available across all management interfaces before moving into the Docker services phase.

---

## Status

| Sub-Phase | Status |
|---|---|
| 4.1 – OPNsense IDS/IPS (Suricata) | 🔲 Not Started |
| 4.2 – Proxmox Host Hardening | 🔲 Not Started |
| 4.3 – Network Segmentation / VLANs | 🔲 Not Started |
| 4.4 – Certificate Management | 🔲 Not Started |
