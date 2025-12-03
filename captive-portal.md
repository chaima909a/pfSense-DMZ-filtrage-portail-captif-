# Portail captif (LAN)

1) Activer
- Services → Captive Portal → Add zone (ex: LAN_PORTAL)
- Interface: LAN, Enable Captive Portal

2) Page de login
- Conserver la page par défaut ou importer HTML perso

3) Comptes
- System → User Manager → Add user

4) Règles LAN
- Supprimer les règles "pass any" directes vers Internet
- Laisser le portail gérer le trafic sortant

5) Tests
- Accès à http://google.com → redirection vers login
- Connexion OK = Internet autorisé pendant la session
