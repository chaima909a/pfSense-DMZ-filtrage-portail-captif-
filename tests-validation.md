# Scénarios de test

- Ping 8.8.8.8 depuis pfSense + VM LAN → OK
- ping google.com (DNS) → OK
- LAN → DMZ:80 → OK (affiche page Apache)
- DMZ → LAN → BLOQUÉ
- DMZ → WAN → OK (apt update)
- Captive Portal: redirection + authentification → OK
- Blocage IP Facebook: ping/HTTP → BLOQUÉ (logs présents)
