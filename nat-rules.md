# NAT sortant & redirections

## NAT sortant
- Rôle : permettre aux IP privées du LAN/DMZ d’accéder à Internet via l’IP WAN.
- Mode : automatique (par défaut) ou manuel si besoin.

## Port forwarding (WAN → DMZ)
- Objectif : publier le serveur web DMZ
- Règle : WAN:80 → 172.16.0.100:80
- Associer une règle firewall WAN correspondante (Pass → 172.16.0.100:80)
