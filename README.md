<div align="center">

<a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&pause=1000&color=D14A4A&center=true&vCenter=true&width=650&lines=SSH;Introduction;Fonctionnement+de+Base;Sécurité+et+Confidentialité" alt="Typing SVG" />
</a>

<p align="center">
  <em>Un dépôt pédagogique autour de SSH.</em><br>
  <b>📘 Apprentissage – 🔐 Sécurité – 🧠 Compréhension</b>
</p>

</div>

---

### 👨‍💻 **À propos de moi.**

> Ce dépôt constitue mon laboratoire numérique où je consigne rigoureusement mes apprentissages et expérimentations. Passionné par l'écosystème Linux > et la cybersécurité, je
> documente mon parcours et mes projets sur mon GitHub. Vous y trouverez des guides pratiques sur la supervision (Zabbix,
> Nagios), la conteneurisation (Docker), la cryptographie les algorithmes de chiffrement symétrique (AES, ChaCha20) et asymétrique (RSA, ECC).  et la
> sécurisation de serveurs Debian. Mon objectif : partager mes connaissances de manière claire et pédagogique. N'hésitez pas à y jeter un œil : https://github.com/0xcyberlitech

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,grafana,prometheus,git,vim" />
  </a>
</p>

---

### 🎯 **Objectif de ce dépôt.**

> Ce dépôt regroupe les notions essentielles sur SSH. Que vous soyez un passionné, un étudiant ou un professionnel, vous y trouverez de quoi comprendre cet outil de sécurité > fondamental, apprendre à le configurer efficacement et maîtriser les bonnes pratiques pour garantir la performance et la stabilité de vos systèmes face aux menaces.

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
