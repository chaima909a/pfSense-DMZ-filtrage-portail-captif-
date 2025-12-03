# Règles principales

1) LAN → DMZ (HTTP uniquement)
- IF: LAN
- SRC: LAN net (192.168.1.0/24)
- DST: 172.16.0.100
- PORT: 80
- ACTION: Pass

2) DMZ → LAN (tout bloqué)
- IF: DMZ
- SRC: DMZ net (172.16.0.0/24)
- DST: LAN net
- ACTION: Block

3) DMZ → WAN (autoriser sortant)
- IF: DMZ
- SRC: DMZ net
- DST: any
- ACTION: Pass

4) Exemple blocage domaine/IP (LAN)
- IF: LAN
- DST: IP Facebook (exemple)
- ACTION: Block + Log
