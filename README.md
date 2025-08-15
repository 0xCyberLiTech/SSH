<div align="center">

  <br></br>
  
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ESSH_" alt="Titre dynamique SSH" />
  </a>
  
  <br></br>
  
  <p align="center">
    <em>Un dépôt pédagogique autour de SSH.</em><br>
    <b>📘 Apprentissage – 🔐 Sécurité – 🧠 Compréhension</b>
  </p>

  [![🌐 Portfolio](https://img.shields.io/badge/Portfolio-0xCyberLiTech-181717?logo=github&style=flat-square)](https://0xcyberlitech.github.io/)
  [![🔗 Profil GitHub](https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square)](https://github.com/0xCyberLiTech)
  [![📦 Dernière version](https://img.shields.io/github/v/release/0xCyberLiTech/SSH?label=version&style=flat-square&color=blue)](https://github.com/0xCyberLiTech/SSH/releases/latest)
  [![📄 CHANGELOG](https://img.shields.io/badge/📄%20Changelog-SSH-blue?style=flat-square)](https://github.com/0xCyberLiTech/SSH/blob/main/CHANGELOG.md)
  [![📂 Dépôts publics](https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square)](https://github.com/0xCyberLiTech?tab=repositories)
  [![👥 Contributeurs](https://img.shields.io/badge/👥%20Contributeurs-cliquez%20ici-007ec6?style=flat-square)](https://github.com/0xCyberLiTech/SSH/graphs/contributors)

</div>

---

### 👨‍💻 **À propos de moi.**

> Bienvenue dans mon **laboratoire numérique personnel** dédié à l’apprentissage et à la vulgarisation de la cybersécurité.  
> Passionné par **Linux**, la **cryptographie** et les **systèmes sécurisés**, je partage ici mes notes, expérimentations et fiches pratiques.  
>  
> Pproposer un contenu clair, structuré et accessible pour étudiants, curieux et professionnels de l’IT.  
> 🔗 [Mon GitHub principal](https://github.com/0xCyberLiTech)

<p align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim" alt="Skills" alt="Logo techno" width="300">
  </a>
</p>

---

### 🎯 **Objectif de ce dépôt.**

> Ce dépôt regroupe les notions essentielles sur SSH. Que vous soyez un passionné, un étudiant ou un professionnel, vous y trouverez de quoi comprendre cet outil de sécurité > fondamental, apprendre à le configurer efficacement et maîtriser les bonnes pratiques pour garantir la performance et la stabilité de vos systèmes face aux menaces.

---

<div align="center" style="margin-bottom: 10px;">

### 🧭 **Sommaire :**

🟢 **Actif** – Dépôt totalement accessible  
🟠 **Partiel** – Dépôt partiellement accessible  
🔴 **Inactif** – Dépôt inaccessible ou indisponible

</div>

---

<div align="center">

| Catégorie | Sujet | Accès Rapide |
|:---:|:---|:---:|
| **SSH** | Plus en détail, qu’est-ce que SSH.| [<img src="https://img.shields.io/badge/EXPLORER-brightgreen?style=for-the-badge&logo=github&logoColor=white">](SSH-INTRODUCTION-IPTABLES.md) |

</div>

---

# Le protocole SSH

## Qu’est-ce que SSH ?

**SSH** (Secure Shell) est un protocole réseau permettant d'établir une connexion sécurisée entre un client et un serveur, principalement pour administrer des systèmes à distance.

---

## Objectifs principaux de SSH :

- **Sécurité** : chiffrer toutes les communications pour éviter l’espionnage.
- **Authentification** : vérifier l’identité du client (et parfois du serveur).
- **Intégrité** : garantir que les données échangées ne sont pas altérées.
- **Confidentialité** : empêcher les interceptions et accès non autorisés.

---

## Comment fonctionne SSH ?

1. **Établissement de la connexion**  
   Le client contacte le serveur SSH sur le port par défaut **22**.

2. **Négociation cryptographique**  
   Le client et le serveur s'accordent sur les algorithmes de chiffrement, de hachage et d’échange de clés.

3. **Authentification**  
   Le client s’authentifie via :
   - Un mot de passe,
   - Ou plus sécurisé : une **clé publique/clé privée** (authentification par clé SSH).

4. **Session sécurisée**  
   Toutes les données échangées (commandes, fichiers) sont chiffrées.

---

## Les avantages de SSH :

- **Sécurité renforcée** par rapport à des protocoles comme Telnet (non chiffré).
- **Multiples usages** : administration distante, transfert de fichiers (SCP, SFTP), tunnels sécurisés.
- **Authentification par clé publique** qui supprime le besoin de mot de passe.
- **Support sur tous les systèmes Unix/Linux** et sur Windows avec des clients compatibles.

---

<p align="center">
  🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessible à tous.
</p>
