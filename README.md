# 🔐 Projet : Infrastructure Réseau Sécurisée avec pfSense

## 🎯 Objectif du projet
Mettre en place une **infrastructure réseau sécurisée et segmentée** basée sur **pfSense** servant de **pare-feu, routeur, serveur DHCP et portail captif**, afin de :
- Séparer les flux entre **LAN**, **DMZ** et **WAN**.
- Contrôler et filtrer l’accès Internet.
- Héberger un **serveur web sécurisé** dans la DMZ.
- Permettre l’authentification des utilisateurs via un **portail captif**.
- Mettre en œuvre des règles **NAT** et **firewall** adaptées à chaque zone.

---

## 🧠 Contexte
Ce projet a été réalisé dans le cadre d’un module de **sécurité des réseaux**.  
L’objectif principal est de **simuler une architecture d’entreprise** typique avec une DMZ, tout en mettant en œuvre des politiques de sécurité et de supervision adaptées.

---

## 🧩 Architecture Réseau

             ┌───────────────┐
             │    Internet    │
             └───────┬───────┘
                     │ (WAN)
            192.168.204.192
                     │
            ┌────────▼────────┐
            │     pfSense     │
            │ (pare-feu / NAT)│
            ├────────┬────────┤
    (LAN)  │192.168.1.1│172.16.0.1│ (DMZ)
            ▼          ▼
 ┌────────────────┐  ┌────────────────┐
 │  PC Client LAN │  │ Serveur Web DMZ│
 │192.168.1.100   │  │172.16.0.100    │
 └────────────────┘  └────────────────┘


 
- **WAN** : accès Internet via réseau externe (192.168.204.0/24)  
- **LAN** : réseau interne des utilisateurs (192.168.1.0/24)  
- **DMZ** : zone hébergeant le serveur web (172.16.0.0/24)

---

## ⚙️ Configuration Technique

### 🔸 Interfaces pfSense
| Interface | Type | IP | Description |
|------------|------|----|-------------|
| em0 | WAN | 192.168.204.192 | Connexion Internet |
| em1 | LAN | 192.168.1.1/24 | Réseau interne |
| em2 | DMZ | 172.16.0.1/24 | Zone démilitarisée |

---

### 🔸 DHCP
- Activé sur **LAN** : 192.168.1.100 → 192.168.1.200  
- Passerelle : 192.168.1.1  
- DNS : 8.8.8.8  

---

### 🔸 NAT (Network Address Translation)
- NAT **sortant** : permet aux machines LAN & DMZ d’accéder à Internet via l’IP WAN.  
- NAT **entrant** : redirection du port **80 (HTTP)** du WAN vers le **serveur web DMZ (172.16.0.100)**.

---

### 🔸 Règles Firewall principales
| Interface | Source | Destination | Port | Action | Description |
|------------|---------|--------------|------|----------|-------------|
| LAN | LAN net | DMZ server (172.16.0.100) | 80 | Pass | Permet accès web interne |
| DMZ | DMZ net | LAN net | any | Block | Empêche trafic vers le LAN |
| DMZ | DMZ net | any | any | Pass | Permet accès Internet |
| WAN | any | DMZ server | 80 | Pass | Redirection HTTP externe |
| LAN | LAN net | facebook.com | any | Block | Exemple de filtrage d’IP/Domaine |

---

### 🔸 Portail Captif (LAN)
1. Activation : **Services → Captive Portal → Add Zone (LAN_PORTAL)**  
2. Interface : **LAN**  
3. Page de connexion : page HTML par défaut  
4. Authentification : via **User Manager** (pfSense local)  
5. Redirection : tout utilisateur non authentifié est redirigé vers la page de login.  

✅ Une fois connecté, il accède librement à Internet.

---

## 💾 Serveur Web dans la DMZ
- Système : **Ubuntu Server 22.04**
- IP : `172.16.0.100`
- Services : **Apache2**
- Fichier de test : `/var/www/html/index.html`
- Objectif : Vérifier la communication LAN → DMZ (port 80)

---

## 🧪 Tests & Validation

| Test | Résultat attendu | Statut |
|------|------------------|--------|
| Ping Internet depuis pfSense | Réussi | ✅ |
| DHCP attribution IP LAN | 192.168.1.x | ✅ |
| Ping Google depuis LAN | OK | ✅ |
| Accès LAN → DMZ:80 | OK (page Apache) | ✅ |
| Accès DMZ → LAN | Bloqué | ✅ |
| NAT : DMZ → Internet | OK | ✅ |
| Captive Portal redirection | Redirection + Login requis | ✅ |
| Blocage domaine Facebook | Accès refusé + Log visible | ✅ |

---

## 🔒 Sécurité & Bonnes Pratiques
- **Segmentation réseau stricte** entre LAN/DMZ/WAN  
- **Blocage des flux non essentiels** (principe du moindre privilège)  
- **Portail captif** pour authentifier les utilisateurs LAN  
- **Règles de filtrage par IP/domaines**  
- **Journalisation (logs)** activée pour les tentatives bloquées  

---

## 🧰 Technologies & Outils
- **pfSense 2.7.x**
- **VMware Workstation**
- **Ubuntu Server 22.04**
- **Apache2**
- **ICMP / DNS / HTTP Tests**

---

## 🧠 Compétences Développées
- Configuration avancée de **pfSense**  
- Mise en place d’une **DMZ sécurisée**  
- Gestion du **NAT, DHCP et firewall**  
- Déploiement d’un **portail captif**  
- Diagnostic réseau et analyse de logs  

---

## 👩‍💻 Auteur
Projet réalisé par **Chayma ABIDI** – 2025  
🎓 Étudiante en Administration & Sécurité des Systèmes Informatiques  


