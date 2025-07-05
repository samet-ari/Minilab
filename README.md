# Minilab
Enterprise Linux Infrastructure with DHCP/DNS/LDAP/NFS

# 🏢 MiniLab - Enterprise Linux Infrastructure

[![Infrastructure](https://img.shields.io/badge/Infrastructure-Enterprise-blue.svg)](https://github.com/samet-ari/Minilab)
[![Services](https://img.shields.io/badge/Services-DHCP%2BDNS%2BLDAP%2BNFS-green.svg)](#)
[![Security](https://img.shields.io/badge/Security-Firewall%2BVPN%2BMFA-red.svg)](#)

## 📋 À Propos du Projet

**Infrastructure réseau Linux de niveau entreprise avec haute disponibilité et services centralisés.**

Implémentation complète d'une infrastructure réseau pour une association utilisant des ordinateurs reconditionnés sous Debian 12.

## 🎯 Technologies Implémentées

- **DHCP**: Master/Slave avec basculement automatique
- **DNS**: Bind9 Master/Slave avec zones forward/reverse  
- **LDAP**: OpenLDAP authentification centralisée (4 utilisateurs)
- **NFS**: Système de fichiers réseau avec RAID 5
- **Sécurité**: Pare-feu + VPN + MFA (Google Authenticator)
- **HA**: Keepalived avec IP virtuelle (99.9% uptime)

## 🏗️ Architecture Réseau
Réseau: 192.168.15.0/24
├── NFS Server (192.168.15.254) - Gateway, Storage, VPN
├── DHCP1 (192.168.15.253) - Services maître
├── DHCP2 (192.168.15.252) - Services esclave
├── Virtual IP (192.168.15.250) - Failover IP
└── DHCP Range (192.168.15.100-150) - Client IPs

## 🚀 Fonctionnalités Clés

- ✅ Basculement automatique (failover)
- ✅ Load balancing DHCP
- ✅ 4 utilisateurs LDAP centralisés
- ✅ Home directories partagés (NFS)
- ✅ Sécurité multi-couches
- ✅ Accès VPN distant (OpenVPN)
- ✅ Tests End-to-End validés

## 📁 Structure du Projet
minilab/
├── README.md
├── configs/
│   ├── dhcp/          # Configurations DHCP et Keepalived
│   ├── dns/           # Configurations DNS et zones
│   ├── ldap/          # Configuration LDAP et utilisateurs
│   ├── nfs/           # Configuration NFS et exports
│   └── security/      # Pare-feu, VPN, MFA
├── documentation/
├── screenshots/
└── scripts/
## 👥 Utilisateurs LDAP Configurés

| Utilisateur | UID | Home Directory | Authentification |
|-------------|-----|----------------|------------------|
| testuser | 10001 | /home/testuser | ✅ LDAP |
| silvia.popescu | 10002 | /home/silvia.popescu | ✅ LDAP |
| pauline.joy | 10003 | /home/pauline.joy | ✅ LDAP |
| samet.ari | 10004 | /home/samet.ari | ✅ LDAP |

## 👤 Auteur

**Samet Ari** - Administrateur Système Linux  
Projet MiniLab - Infrastructure Linux Entreprise

---
