# cisco-collapsed-core-vlsm-network
Cisco enterprise network architecture simulation on Packet Tracer using a Collapsed Core design and VLSM addressing
# Architecture Réseau Cisco - Modèle Hiérarchique Collapsed Core & VLSM

Ce projet présente la conception, l'implémentation et la sécurisation d'une infrastructure réseau complète adaptée à une moyenne entreprise (PME). Développée sur **Cisco Packet Tracer**, cette topologie optimise l'espace d'adressage IP et centralise la gestion du trafic de manière professionnelle.

## 📊 Topologie du Réseau
Network-topology.png

## 🛠️ Concepts & Technologies Implémentés

* **Architecture Collapsed Core (Cœur effondré) :** Choix d'un design en étoile à deux couches (Accès et Distribution/Cœur fusionnés) parfaitement adapté à une entreprise de taille moyenne. Centralisation de la topologie autour d'un switch principal.
* **Routage Inter-VLAN (Router-on-a-Stick) :** Configuration de sous-interfaces d'encapsulation `802.1Q` sur une seule interface physique du routeur central (`G0/0/1`).
* **Adressage VLSM (Variable Length Subnet Mask) :** Découpage optimal d'un bloc IP de classe C pour répondre aux besoins précis de chaque zone (30 hôtes et 14 hôtes) sans gaspillage, avec des masques en `/27` et `/28`.
* **Services Réseau :** Centralisation et automatisation de l'adressage des clients via des pools **DHCP** configurés directement sur le routeur pour chaque VLAN.
* **Sécurisation & Durcissement (Hardening) :**
  * Isolation complète des équipements de commutation via un réseau de gestion dédié (**VLAN 99**).
  * Modification du **VLAN Natif (VLAN 100)** sur l'ensemble des liaisons Trunks pour contrer les attaques de type *VLAN Hopping*.
  * Chiffrement des mots de passe globaux (`service password-encryption`).
  * Activation exclusive du protocole sécurisé **SSHv2** pour l'administration distante (VTY).

## 🔀 Plan d'Adressage IP (VLSM)

| Zone / VLAN | Rôle | Adresse Réseau | Masque | Passerelle (Routeur) | Plage Utile |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **VLAN 40** (Rose) | Zone 30 Hôtes | `192.168.1.64` | `/27` | `192.168.1.94` | `.65` à `.93` |
| **VLAN 50** (Kaki) | Zone 30 Hôtes | `192.168.1.96` | `/27` | `192.168.1.126` | `.97` à `.125` |
| **VLAN 10** (Bleu) | Zone 14 Hôtes | `192.168.1.128` | `/28` | `192.168.1.142` | `.129` à `.141` |
| **VLAN 20** (Violet) | Zone 14 Hôtes | `192.168.1.144` | `/28` | `192.168.1.158` | `.145` à `.157` |
| **VLAN 30** (Vert) | Zone 14 Hôtes | `192.168.1.160` | `/28` | `192.168.1.174` | `.161` à `.173` |
| **VLAN 99** (Gris) | Management | `192.168.1.176` | `/28` | `192.168.1.190` | `.177` à `.189` |

## ⚙️ Fichiers de Configuration

Les fichiers complets d'exécution de la topologie sont disponibles dans le dossier `/configs`. Voici un aperçu des principaux équipements :

<details>
<summary>💻 Cliquez pour voir la configuration finale du Routeur (R1)</summary>

```cisco
! Insère ici ta configuration complète de routeur si tu le souhaites ou laisse les fichiers dans /configs
