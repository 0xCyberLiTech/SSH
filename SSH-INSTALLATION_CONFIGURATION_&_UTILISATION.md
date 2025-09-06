<div align="center">

  <br></br>
  
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ESSH_" alt="Titre dynamique SSH" />
  </a>
  
  <br></br>
  
  <h2>Laboratoire numérique pour la cybersécurité, Linux & IT.</h2>

  <p align="center">
    <a href="https://0xcyberlitech.github.io/">
      <img src="https://img.shields.io/badge/Portfolio-0xCyberLiTech-181717?logo=github&style=flat-square" alt="🌐 Portfolio" />
    </a>
    <a href="https://github.com/0xCyberLiTech">
      <img src="https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square" alt="🔗 Profil GitHub" />
    </a>
    <a href="https://github.com/0xCyberLiTech/SSH/releases/latest">
      <img src="https://img.shields.io/github/v/release/0xCyberLiTech/SSH?label=version&style=flat-square&color=blue" alt="📦 Dernière version" />
    </a>
    <a href="https://github.com/0xCyberLiTech/SSH/blob/main/CHANGELOG.md">
      <img src="https://img.shields.io/badge/📄%20Changelog-SSH-blue?style=flat-square" alt="📄 CHANGELOG SSH" />
    </a>
    <a href="https://github.com/0xCyberLiTech?tab=repositories">
      <img src="https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square" alt="📂 Dépôts publics" />
    </a>
    <a href="https://github.com/0xCyberLiTech/SSH/graphs/contributors">
      <img src="https://img.shields.io/badge/👥%20Contributeurs-cliquez%20ici-007ec6?style=flat-square" alt="👥 Contributeurs SSH" />
    </a>
  </p>

</div>

<div align="center">
  <img src="https://img.icons8.com/fluency/96/000000/cyber-security.png" alt="CyberSec" width="80"/>
</div>

<div align="center">
  <p>
    <strong>Cybersécurité</strong> <img src="https://img.icons8.com/color/24/000000/lock--v1.png"/> • <strong>Linux Debian</strong> <img src="https://img.icons8.com/color/24/000000/linux.png"/> • <strong>Sécurité informatique</strong> <img src="https://img.icons8.com/color/24/000000/shield-security.png"/>
  </p>
</div>

---

<div align="center">
  
## À propos & Objectifs.

</div>

Ce projet propose des solutions innovantes et accessibles en cybersécurité, avec une approche centrée sur la simplicité d’utilisation et l’efficacité. Il vise à accompagner les utilisateurs dans la protection de leurs données et systèmes, tout en favorisant l’apprentissage et le partage des connaissances.

Le contenu est structuré, accessible et optimisé SEO pour répondre aux besoins de :
- 🎓 Étudiants : approfondir les connaissances
- 👨‍💻 Professionnels IT : outils et pratiques
- 🖥️ Administrateurs système : sécuriser l’infrastructure
- 🛡️ Experts cybersécurité : ressources techniques
- 🚀 Passionnés du numérique : explorer les bonnes pratiques

---

# 🔐 TP SSH — Installation, Configuration et Utilisation

## 📑 Sommaire
- [Introduction](#introduction)
- [Chapitre 1 : Installation et Configuration](#chapitre-1--installation-et-configuration)
  - [1. Installation du serveur SSH](#1-installation-du-serveur-ssh)
  - [2. Fichiers de configuration](#2-fichiers-de-configuration)
  - [3. Exemple de configuration de base](#3-exemple-de-configuration-de-base)
  - [4. Exemple de configuration avancée](#4-exemple-de-configuration-avancée)
  - [5. Mise en place de clés SSH](#5-mise-en-place-de-clés-ssh)
  - [6. Sécurisation supplémentaire](#6-sécurisation-supplémentaire)
- [Chapitre 2 : Utilisation pratique de SSH et SCP](#chapitre-2--utilisation-pratique-de-ssh-et-scp)
  - [1. Connexion à un serveur](#1-connexion-à-un-serveur)
  - [2. Exécuter une commande distante](#2-exécuter-une-commande-distante)
  - [3. Transfert de fichiers avec SCP](#3-transfert-de-fichiers-avec-scp)
  - [4. Synchronisation avec Rsync](#4-synchronisation-avec-rsync)
  - [5. Tunnel SSH](#5-tunnel-ssh)
  - [6. Utilisation d’une clé privée](#6-utilisation-dune-clé-privée)
- [Récapitulatif des commandes](#récapitulatif-des-commandes)
- [Conclusion](#conclusion)

---

## Introduction

**SSH (Secure Shell)** est un protocole permettant :  
- Une **connexion sécurisée** à distance à une machine (administration système).  
- Le **transfert de fichiers chiffrés** (`scp`, `sftp`).  
- La création de **tunnels sécurisés** pour rediriger des services réseau.  

Il fonctionne par défaut sur le **port 22**, mais il est recommandé de le changer pour limiter les attaques automatisées.

---

# Chapitre 1 — Installation et Configuration

## 1. Installation du serveur SSH

### Debian / Ubuntu
```bash
sudo apt update && sudo apt install -y openssh-server
sudo systemctl enable --now ssh
```

### RedHat / CentOS / Fedora
```bash
sudo dnf install -y openssh-server
sudo systemctl enable --now sshd
```

Vérifier que le service tourne :
```bash
systemctl status ssh
```

---

## 2. Fichiers de configuration

Fichier principal :  
```bash
/etc/ssh/sshd_config
```

| Paramètre | Rôle | Exemple |
|-----------|------|---------|
| `Port` | Définit le port SSH | `Port 2222` |
| `PermitRootLogin` | Autorise/refuse root | `PermitRootLogin no` |
| `PasswordAuthentication` | Active/désactive les mots de passe | `PasswordAuthentication no` |
| `AllowUsers` | Utilisateurs autorisés | `AllowUsers admin user1` |
| `AllowGroups` | Groupes autorisés | `AllowGroups admins` |

⚠️ Après modification :  
```bash
sudo systemctl restart ssh
```

---

## 3. Exemple de configuration de base
```conf
Port 2222
PermitRootLogin no
PasswordAuthentication yes
AllowUsers admin
```

---

## 4. Exemple de configuration avancée
```conf
Port 2222
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AllowGroups admins
MaxAuthTries 3
LoginGraceTime 30
ClientAliveInterval 300
ClientAliveCountMax 2
```

**Explication terrain** :  
- `PasswordAuthentication no` → empêche les attaques par force brute.  
- `PubkeyAuthentication yes` → authentification uniquement par clé publique.  
- `MaxAuthTries 3` → limite les tentatives de connexion.  

---

## 5. Mise en place de clés SSH

### Générer une clé sur le client
```bash
ssh-keygen -t rsa -b 4096 -C "admin@pc"
```

### Copier la clé sur le serveur
```bash
ssh-copy-id -p 2222 admin@192.168.1.10
```

### Connexion sans mot de passe
```bash
ssh -p 2222 admin@192.168.1.10
```

---

## 6. Sécurisation supplémentaire

- **Fail2ban (bloquer les IP malveillantes)**
  ```bash
  sudo apt install fail2ban
  ```

- **Firewall UFW**
  ```bash
  sudo ufw allow 2222/tcp
  sudo ufw enable
  ```

---

# Chapitre 2 — Utilisation pratique de SSH et SCP

## 1. Connexion à un serveur
```bash
ssh admin@192.168.1.10
```

---

## 2. Exécuter une commande distante
```bash
ssh admin@192.168.1.10 "uptime"
```

---

## 3. Transfert de fichiers avec SCP

### Local → Distant
```bash
scp fichier.txt admin@192.168.1.10:/home/admin/
```

### Distant → Local
```bash
scp admin@192.168.1.10:/home/admin/log.txt ./log.txt
```

### Copier un dossier
```bash
scp -r sauvegarde/ admin@192.168.1.10:/home/admin/backups/
```

---

## 4. Synchronisation avec Rsync
```bash
rsync -avz projet/ admin@192.168.1.10:/home/admin/projets/
```

---

## 5. Tunnel SSH
Rediriger un port local vers un service distant :
```bash
ssh -L 8080:localhost:80 admin@192.168.1.10
```
👉 Permet d’accéder au port 80 du serveur via `http://localhost:8080`

---

## 6. Utilisation d’une clé privée
```bash
ssh -i ~/.ssh/id_rsa admin@192.168.1.10
```

---

# Récapitulatif des commandes

| Action | Commande | Exemple |
|--------|----------|---------|
| Connexion simple | `ssh user@ip` | `ssh admin@192.168.1.10` |
| Connexion avec port | `ssh -p port user@ip` | `ssh -p 2222 admin@192.168.1.10` |
| Commande distante | `ssh user@ip "cmd"` | `ssh admin@192.168.1.10 "uptime"` |
| Copier fichier local → distant | `scp fichier user@ip:/path/` | `scp notes.txt admin@192.168.1.10:/home/admin/` |
| Copier fichier distant → local | `scp user@ip:/fichier /local/` | `scp admin@192.168.1.10:/home/admin/log.txt ./` |
| Copier dossier | `scp -r dossier user@ip:/path/` | `scp -r sauvegarde/ admin@192.168.1.10:/home/admin/backups/` |
| Synchroniser | `rsync -avz src user@ip:/path/` | `rsync -avz /var/www/ admin@192.168.1.10:/home/admin/www/` |
| Tunnel SSH | `ssh -L port_local:localhost:port_distant user@ip` | `ssh -L 8080:localhost:80 admin@192.168.1.10` |
| Copier clé publique | `ssh-copy-id user@ip` | `ssh-copy-id admin@192.168.1.10` |

---

# ✅ Conclusion

- **Chapitre 1** : Installation, configuration et sécurisation du serveur SSH.  
- **Chapitre 2** : Utilisation pratique (connexion, transferts, tunnels, automatisation).  

👉 Avec cette base, un administrateur système peut :  
- Gérer ses serveurs Linux à distance en toute sécurité.  
- Automatiser des transferts et synchronisations fiables.  
- Mettre en place un SSH renforcé contre les attaques courantes.  

---

<div align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="440">
  </a>
</div>

<div align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</div>

