# Configuration-d-EtherChannel-avec-PAgP-et-LACP
📚 Description
Ce projet présente la configuration d'EtherChannel sur trois commutateurs (SWA, SWB, SWC) en utilisant :
PAgP (Port Aggregation Protocol) : Protocole propriétaire Cisco
LACP (Link Aggregation Control Protocol) : Standard IEEE 802.3ad
L'objectif est d'améliorer la bande passante, d'augmenter la redondance et de simplifier la gestion des liens.

🧩 Topologie


🔧 Configuration réalisée
Port-Channel	Appareils	Interfaces utilisées	Protocole	Mode utilisé
1	SWA ↔ SWB	G0/1 - G0/2	PAgP	desirable / auto
2	SWA ↔ SWC	F0/21 - F0/22	LACP	active / active
3	SWB ↔ SWC	F0/23 - F0/24	LACP	passive / active
⚙️ Commandes principales

1. Configuration du trunk
bash
Copier
Modifier
interface range GigabitEthernet0/1 - 2
switchport mode trunk

2. Configuration d'un Port-Channel PAgP (SWA ↔ SWB)
bash
Copier
Modifier
interface range GigabitEthernet0/1 - 2
channel-group 1 mode desirable
bash
Copier
Modifier
interface range GigabitEthernet0/1 - 2 (sur SWB)
channel-group 1 mode auto

3. Configuration d'un Port-Channel LACP (SWA ↔ SWC)
bash
Copier
Modifier
interface range FastEthernet0/21 - 22
switchport mode trunk
channel-group 2 mode active

4. Configuration d'un Port-Channel LACP (SWB ↔ SWC)
bash
Copier
Modifier
interface range FastEthernet0/23 - 24
switchport mode trunk
channel-group 3 mode passive
bash
Copier
Modifier
interface range FastEthernet0/23 - 24 (sur SWC)
channel-group 3 mode active

🔍 Vérifications
Utiliser les commandes suivantes :

show etherchannel summary ➔ Résumé des EtherChannel actifs

show interfaces trunk ➔ Vérification des trunks

show running-config ➔ Vérification de la configuration

show etherchannel detail ➔ Détail sur les Port-Channels

📦 Résultat attendu
Chaque Port-Channel doit être UP et les liens doivent être agrégés correctement.

Les trunks doivent transporter tous les VLANs nécessaires.

La redondance doit être assurée : si un lien tombe, les autres prennent le relais.

