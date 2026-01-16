# 🔧 Infra Réseau d’Entreprise – Proxmox | AD/DNS/DHCP | NAS | Firewall/Routeur virtuels | Wi‑Fi | Impression

> Projet d’infrastructure pour PME : 3 hôtes Proxmox en cluster (HA), NAS partagé (Commun/Finance/Marketing, Backups, Perso), services Windows (AD/DNS/DHCP + redondance), serveur Linux (site web), pare‑feu & routeur virtuels, switch physique, points d’accès Wi‑Fi, serveur d’impression.
## 🧭 Sommaire
- Objectifs
- Périmètre
- Architecture
- Plan d’adressage & VLAN
- Structure des partages NAS
- Déploiement – Pas à pas
- Sécurité
- Sauvegardes & PRA
- Supervision
- User Stories (IceScrum)
- Arborescence du repo
- Exploitation (Runbook)
- Contribuer
- Licence

## 🎯 Objectifs
- Haute disponibilité via cluster Proxmox (3 nœuds).
- Services cœur d’infra : AD / DNS / DHCP, second DC pour redondance.
- NAS centralisé : Commun/Finance/Marketing, Backups, Perso.
- Pare‑feu & routeur virtuels.
- Site web interne/externe sur Linux (HTTPS).
- Réseau filaire + Wi‑Fi segmenté (Employés / Invités).
- Serveur d’impression.

## 📦 Périmètre
- 3 serveurs physiques → Proxmox VE + NAS partagé.
- VM Windows #1 : AD DS, DNS, DHCP.
- VM Windows #2 : DC secondaire.
- VM Linux : site web.
- Pare‑feu virtuel & routeur virtuel.
- Switch physique, AP Wi‑Fi, serveur d’impression.

## 🏗 Architecture
(Diagramme Mermaid non inclus dans ce fichier, mais présent dans les docs du projet.)

## 🌐 Plan d’adressage & VLAN
- VLAN 10 – Management
- VLAN 20 – Serveurs
- VLAN 30 – Utilisateurs
- VLAN 40 – Wi‑Fi Invités
- VLAN 50 – Sauvegardes
- DMZ – Web

## 🗂 Structure des partages NAS
NAS
 ├─ Commun
 │   ├─ Finance
 │   └─ Marketing
 ├─ Backup
 │   ├─ Proxmox
 │   └─ Serveurs
 └─ Perso
     └─ username
## Déploiement – Pas à pas
### 1) Proxmox
- Installation des trois hôtes.
- Création du cluster.
- Activation HA.

### 2) NAS
- Création des partages.
- ACL via AD.

### 3) AD/DNS/DHCP
- Promotion DC1 & DC2.
- DNS internalisé.
- DHCP centralisé.

### 4) Linux Web
- Installation Nginx/Apache.
- HTTPS.

### 5) Réseau
- Pare-feu.
- Routeur.
- VLANs.

## 🔐 Sécurité
- MFA.
- VLAN séparés.
- Mises à jour régulières.
- Journaux centralisés.

## 💾 Sauvegardes & PRA
- Backups Proxmox → NAS.
- Tests de restauration.
- Documentation PRA.

## 📈 Supervision
- Zabbix / Grafana.
- Alertes serveurs.
- Monitoring réseau.

## 🗃 Arborescence du repo
```
.
├─ docs/
├─ agile/
├─ scripts/
└─ README.md
```

## 🤝 Contribuer
1. Fork.
2. Branche `feat/*` ou `fix/*`.
3. Pull request.

## 📄 Licence
MIT.
