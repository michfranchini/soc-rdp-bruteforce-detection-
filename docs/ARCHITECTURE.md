Lab Network Architecture

| Host | Role | Key Configuration | Network |
| --- | --- | --- | --- |
| `KALI.LAB.LOCAL` (192.168.1.10) | Attacker | Hydra for RDP brute-force | LAN (via PfSense) |
| `CYBERSECVICTIM.LAB.LOCAL` (192.168.1.20) | Target | Windows 10, RDP enabled, **NLA disabled (intentionally vulnerable)**, weak creds | LAN (via PfSense) |
| `WAZUH.LAB.LOCAL` (192.168.1.30) | SIEM | Wazuh Manager + Dashboard, AlmaLinux 9 | LAN (via PfSense) |
| `DC.LAB.LOCAL` (192.168.1.2) | Domain Controller | Windows Server 2022, AD, DNS | LAN (via PfSense) |
| `PFSENSE.LAB.LOCAL` (192.168.1.1) | Firewall/Router | PfSense CE, NAT, LAN/WAN | LAN (192.168.1.0/24), WAN (DHCP) |

* **Network**: All hosts are on the same LAN segment (`192.168.1.0/24`) managed by PfSense.
* **Domain**: `LAB.LOCAL` domain with `DC.LAB.LOCAL` as primary DC (though not used in detection).
* **Detection Flow**: Attack → Target → Wazuh Agent (Win10) → Wazuh Manager (AlmaLinux) → Alert.

**Note**: The Domain Controller was part of the lab setup but did not directly impact this detection. It was used for centralized authentication and domain management.
