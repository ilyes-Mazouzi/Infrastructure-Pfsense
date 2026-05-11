🛡️ Infrastructure pfSense — Lab Personnel

Simulation d'une infrastructure réseau d'entreprise virtualisée sous VMware, avec segmentation réseau par interfaces dédiées, Active Directory, pare-feu pfSense et GPO.

📋 Objectif
Reproduire l'infrastructure réseau d'une PME avec 3 services distincts (RH, Finance, Informatique), une gestion centralisée des utilisateurs via Active Directory, et une segmentation réseau sécurisée via pfSense.

🖧 Architecture réseau

<img width="399" height="321" alt="image" src="https://github.com/user-attachments/assets/17699cbd-b7a8-428f-b061-018629e9fb37" />




📁 Active Directory
Domaine : pfsense.local
Structure des OUs
<img width="1026" height="778" alt="OU" src="https://github.com/user-attachments/assets/0a122503-3666-470d-b382-68beae3088f2" />



<img width="235" height="210" alt="image" src="https://github.com/user-attachments/assets/cd649d2c-67a8-4dd7-9c18-664977ba918b" />


Groupe RH
<img width="1028" height="778" alt="RH" src="https://github.com/user-attachments/assets/555fe8c0-1732-4e97-aaa9-bb527544ed3d" />

Groupe Finance
<img width="1025" height="769" alt="finance" src="https://github.com/user-attachments/assets/e6b548e6-44bd-4695-b32b-365e1a3ae335" />

Groupe Technicien
<img width="1026" height="772" alt="tech" src="https://github.com/user-attachments/assets/38266acf-c2e1-4efe-bced-76aa1ce38cd4" />


🔌 pfSense — Interfaces & DHCP
Interface Assignments

<img width="1032" height="771" alt="pfsense gui" src="https://github.com/user-attachments/assets/2a48d053-1f63-49ae-bb1e-4edc47e4370b" />




DHCP RH (10.0.10.50 → 10.0.10.150)
<img width="1023" height="773" alt="RH pfsense" src="https://github.com/user-attachments/assets/250b6136-ceb5-4ae5-af20-1103cbd9a091" />



DHCP Finance (10.0.20.50 → 10.0.20.150)
<img width="1028" height="772" alt="finance pfsense" src="https://github.com/user-attachments/assets/113b9ae4-5140-4000-aa4c-799d21b2054a" />



DHCP Technicien (10.0.30.50 → 10.0.30.150)
<img width="1025" height="771" alt="tech pfsense" src="https://github.com/user-attachments/assets/7d859180-c4f5-4164-b213-78ad105f0b2d" />


🔒 Règles Firewall
Principe appliqué : "deny specific, allow all" — les règles de blocage sont placées en priorité, suivies d'une règle d'autorisation générale.

RH — Bloque Finance, autorise le reste
<img width="1034" height="782" alt="rules rh" src="https://github.com/user-attachments/assets/a20d7cfc-bdc2-4587-a8c5-1e5f796c31b8" />

Finance — Bloque RH, autorise le reste
<img width="1031" height="767" alt="rules finance" src="https://github.com/user-attachments/assets/8bd79e58-bd7c-4445-9a70-3c5f2d2d7cf1" />

Technicien — Accès total (rôle admin)
<img width="1005" height="385" alt="rules tech" src="https://github.com/user-attachments/assets/05475528-a091-418d-bd4c-395ce144f5aa" />

✅ Tests de validation

IPs clients par réseau
Client RH — 10.0.10.50
<img width="982" height="510" alt="rh ip" src="https://github.com/user-attachments/assets/4b71409e-0403-4191-8802-42ef66e4c84e" />

Client Finance — 10.0.30.50
<img width="987" height="516" alt="finance ip" src="https://github.com/user-attachments/assets/4a418643-b1d7-4865-944b-fff5143d6e5a" />

Client Technicien — 10.0.20.50
<img width="979" height="513" alt="tech ip" src="https://github.com/user-attachments/assets/5e0914fc-f1a0-4835-9312-ac3c9b29eaea" />

Tests de blocage inter-réseaux
RH → Finance : bloqué ❌
<img width="978" height="511" alt="ping rh vers finance" src="https://github.com/user-attachments/assets/7fbbd670-3901-4ecf-9d14-3fc6a493c1c6" />

Finance → RH : bloqué ❌
<img width="979" height="513" alt="ping finance vers rh" src="https://github.com/user-attachments/assets/f040d8b8-4ec2-460f-80e2-65082aacd8d3" />

⚙️ GPO configurées
Politique de mot de passe (Default Domain Policy)

<img width="1023" height="769" alt="mot de passe gpo" src="https://github.com/user-attachments/assets/9d950580-919d-4587-a908-3c56d6453bef" />

Restriction fond d'écran (OU RH)
Les utilisateurs RH ne peuvent pas modifier leur fond d'écran.

<img width="1023" height="763" alt="fond d&#39;ecran rh" src="https://github.com/user-attachments/assets/431b36a9-23d6-46b4-81b7-658b18b4d924" />


📚 Ce que j'ai appris

Configuration d'un pare-feu pfSense (WAN/LAN, interfaces, NAT)
Segmentation réseau par interfaces physiques dédiées
Déploiement d'un Active Directory (AD DS, DNS, DHCP) sur Windows Server 2022
Création d'OUs, groupes et utilisateurs dans l'AD
Application de GPO (politique de mot de passe, restriction utilisateur)
Mise en place de règles firewall avec ordre de priorité
Compréhension de l'architecture réseau d'une PME


🔧 Difficultés rencontrées

Ordre des règles pfSense : les règles firewall sont lues de haut en bas, une règle ALLOW placée avant un BLOCK annule le blocage. Correction par réorganisation manuelle des règles.
Jointure de domaine : les clients doivent être sur le même réseau que le serveur AD pour rejoindre le domaine, ou avoir une route vers lui.
VLANs vs interfaces physiques : dans VMware, les VLANs nécessitent un switch virtuel manageable. Remplacement par des interfaces physiques dédiées pour simuler la segmentation.


Lab réalisé dans le cadre d'une montée en compétences personnelle — Mai 2026













