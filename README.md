# 🔐 Réseau sécurisé avec pfSense : DMZ, filtrage, NAT & portail captif

Architecture avec **pfSense** servant de routeur/pare-feu (WAN/LAN/DMZ), **NAT** sortant,
**DMZ** isolée pour un serveur web Apache, et **portail captif** sur le LAN.

- Hyperviseur : VMware Workstation
- pfSense :
  - WAN : 192.168.204.192
  - LAN : 192.168.1.1/24
  - DMZ : 172.16.0.1/24
- VM LAN (ex. nginx01) : IP via DHCP pfSense (ex. 192.168.1.100)
- VM DMZ (Ubuntu) : 172.16.0.100, Apache2

Fonctions clés : **NAT**, **DHCP LAN**, **règles firewall segmentées**, **portail captif**.
