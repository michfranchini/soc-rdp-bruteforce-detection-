Lab Network Architecture

| Host | Role | Key Configuration | Network |
| --- | --- | --- | --- |
| `KALI.LAB.LOCAL` (10.0.20.201) | Attacker | Hydra for RDP brute-force | LAN (via PfSense) |
| `CYBERSECVICTIM.LAB.LOCAL` (10.0.10.20) | Target | Windows 10, RDP enabled, **NLA disabled (intentionally vulnerable)**, weak creds | LAN (via PfSense) |
| `WAZUH.LAB.LOCAL` (10.0.10.5) | SIEM | Wazuh Manager + Dashboard, AlmaLinux 9 | LAN (via PfSense) |
| `DC.LAB.LOCAL` (10.0.10.10) | Domain Controller | Windows Server 2022, AD, DNS | LAN (via PfSense) |
| `PFSENSE.LAB.LOCAL` (10.0.2.15) | Firewall/Router | PfSense CE, NAT, LAN/WAN | LAN (10.0.10.0/24), WAN (DHCP) |

* **Network**: All hosts except Kali are on the same LAN segment (`10.0.10.0/24`) managed by PfSense.
* **Domain**: `LAB.LOCAL` domain with `DC.LAB.LOCAL` as primary DC (though not used in detection).
* **Detection Flow**: Attack → Target → Wazuh Agent (Win10) → Wazuh Manager (AlmaLinux) → Alert.

**Note**: The Domain Controller was part of the lab setup but did not directly impact this detection. It was used for centralized authentication and domain management.
