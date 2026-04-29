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

# Générer une paire de clés SSH sous Linux

*Pôle Cyber – Fait le 28-04-2026*

## 1. Génération de la paire de clés SSH

**Machine locale (Linux Debian) :** 10.10.10.101  
**Serveur distant (Linux Debian) :** 10.10.10.102

Pour générer une paire de clés SSH :

```bash
ssh-keygen
```

Par défaut, une clé RSA de 2048 bits est créée. Pour une clé de taille différente :

```bash
ssh-keygen -b 4096
```

L’utilitaire vous demandera où enregistrer la clé (par défaut : `~/.ssh/id_rsa`).

- Pour root : `/root/.ssh`
- Pour un utilisateur : `/username/.ssh`

Il est conseillé de garder l’emplacement par défaut.

Si une clé existe déjà :

```
/home/username/.ssh/id_rsa already exists.
Overwrite (y/n)?
```

Attention : écraser la clé supprimera l’ancienne (action irréversible).

Vous pouvez ensuite définir une phrase de passe (optionnelle) pour protéger la clé privée.

### Avantages d’une phrase de passe :
- La clé privée n’est jamais exposée sur le réseau.
- La phrase de passe protège la clé sur la machine locale.
- Les droits d’accès restreints protègent la clé.
- Un attaquant doit déjà avoir accès à votre compte pour tenter de casser la phrase de passe.
- La phrase de passe offre une protection supplémentaire en cas de compromission.

Si vous ne souhaitez pas de phrase de passe, appuyez sur ENTER.

Après création, les clés sont dans `~/.ssh` :
- `id_xxx` : clé privée
- `id_xxx.pub` : clé publique

Pour vérifier :

```bash
cd ~/.ssh
ls
id_ed25519
id_ed25519.pub
```

## 2. Transférer la clé publique vers le serveur distant

Depuis la machine locale, transférez la clé publique :

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub -p 2272 root@10.10.10.102
```

Une authentification sera demandée. La clé sera copiée dans `~/.ssh/authorized_keys` sur le serveur distant.

## 3. Vérifier et sécuriser les droits d’accès

Connectez-vous en SSH :

```bash
ssh -p 2272 root@10.10.10.102
```

Sécurisez les droits :

```bash
cd /root/
chmod 700 .ssh/
cd /root/.ssh/
chmod 600 authorized_keys
```

Redémarrez le service SSH :

```bash
systemctl restart ssh.service
```

Vous pouvez maintenant vous connecter sans mot de passe :

```bash
ssh -p 2272 root@10.10.10.102
```

## 4. Modifier la configuration SSH

Pour renforcer la sécurité, modifiez `/etc/ssh/sshd_config` :

```conf
# Authentication:
LoginGraceTime 1m
#PermitRootLogin prohibit-password
PermitRootLogin yes
#StrictModes yes
MaxAuthTries 4
MaxSessions 2

PubkeyAuthentication yes

# Pour désactiver l’authentification par mot de passe :
PasswordAuthentication no
```

> **Attention** : Avec `PasswordAuthentication no`, la connexion SSH par mot de passe est désactivée.

---

<div align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="440">
  </a>
</div>

<div align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</div>
