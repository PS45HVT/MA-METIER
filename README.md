

\# 🔧 Infra Réseau d’Entreprise – Proxmox | AD/DNS/DHCP | NAS | Firewall/Routeur virtuels | Wi‑Fi | Impression



> Projet d’infrastructure pour PME : 3 hôtes Proxmox en cluster (HA), NAS partagé (Commun/Finance/Marketing, Backups, Perso), services Windows (AD/DNS/DHCP + redondance), serveur Linux (site web), pare‑feu \& routeur virtuels, switch physique, points d’accès Wi‑Fi, serveur d’impression.



!Status

!Infra

!\[License](https://img.shields.io/bs- \[Objectifs](#-objectre](#Architecture](#-lan d’adressage \& VLAN](#-plan-de des partages NAS

\- Déploiement – Pas à pas

\- Sécurité

\- Sauvegardes \& PRA

\- Supervision

\- User Stories (IceScrum)

\- Arborescence du repo

\- Exploitation (Runbook)

\- Contribuer

\- Licence



---



\## 🎯 Objectifs

\- Haute disponibilité via \*\*cluster Proxmox (3 nœuds)\*\*.

\- Services cœur d’infra : \*\*AD / DNS / DHCP\*\*, \*\*second DC\*\* pour redondance.

\- \*\*NAS centralisé\*\* : dossiers \*Commun/Finance/Marketing\*, \*Backups\*, \*Perso\* (intégration AD).

\- \*\*Pare‑feu \& routeur\*\* virtuels (segmentation / filtrage / NAT / DMZ).

\- \*\*Site web\*\* interne/externe sur Linux (HTTPS).

\- \*\*Réseau filaire + Wi‑Fi\*\* segmenté (Employés / Invités).

\- \*\*Serveur d’impression\*\* avec déploiement GPO.

\- Supervision, sauvegardes et \*\*PRA\*\* documentés.



---



\## 📦 Périmètre

\- \*\*3 serveurs physiques\*\* → Proxmox VE + stockage partagé (NAS NFS/iSCSI)  

\- \*\*VM Windows\*\* #1 : AD DS, DNS, DHCP  

\- \*\*VM Windows\*\* #2 : Contrôleur de domaine secondaire (redondance)  

\- \*\*VM Linux\*\* : site web (Nginx/Apache)  

\- \*\*Pare‑feu virtuel\*\* (OPNsense/pfSense) \& \*\*Routeur virtuel\*\*  

\- \*\*Switch physique\*\*, \*\*AP Wi‑Fi\*\*, \*\*serveur d’impression\*\*  

\- \*\*NAS\*\* : Commun (Finance/Marketing), Backups, Perso



---



\## 🏗 Architecture



\### Diagramme logique (Mermaid)

```mermaid

flowchart LR

&nbsp; subgraph Users\[Utilisateurs]

&nbsp;   PC1\[Postes fixes]

&nbsp;   LAP1\[Laptops]

&nbsp;   WIFI\[Wi‑Fi: AP]

&nbsp; end



&nbsp; subgraph Core\[Datacenter - Proxmox Cluster (3 nœuds)]

&nbsp;   PVE1\[PVE-01]

&nbsp;   PVE2\[PVE-02]

&nbsp;   PVE3\[PVE-03]



&nbsp;   FW\[FW virtuel]

&nbsp;   RT\[Routeur virtuel]

&nbsp;   DC1\[Windows Server - AD/DNS/DHCP]

&nbsp;   DC2\[Windows Server - AD secondaire]

&nbsp;   WEB\[Linux - Site Web]

&nbsp;   PRINT\[Serveur d'impression]

&nbsp; end



&nbsp; NAS\[(NAS - NFS/SMB/iSCSI)]

&nbsp; SW\[Switch Physique]



&nbsp; Users --> SW

&nbsp; SW <---> Core

&nbsp; Core <---> NAS



&nbsp; FW <---> RT

&nbsp; FW -->|NAT/Filtrage| Internet\[(Internet)]

&nbsp; RT -->|Routage Inter-VLAN| DC1

&nbsp; RT --> WEB

&nbsp; RT --> PRINT



&nbsp; DC1 <--replication--> DC2

&nbsp; WEB -->|HTTPS| FW



