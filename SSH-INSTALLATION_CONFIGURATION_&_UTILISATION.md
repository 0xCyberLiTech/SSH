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

# Connexion SSH — Windows (PowerShell) → Serveur Linux

But : Générer une paire ed25519 sur le client Windows, charger la clé privée dans l'agent (passphrase saisie une seule fois), copier la clé publique sur le serveur et tester la connexion.

---

## 1) Générer la paire (PowerShell)

Exécutez dans PowerShell (session utilisateur) :

```powershell
ssh-keygen -t ed25519 -C "srv-linux" -f "$env:USERPROFILE\.ssh\id_ed25519"
```

Quand on vous demande une passphrase, pour l'exemple pédagogique utilisez :

```
Jesuisenweekenddans6h00cestsuper
```

Remarque : c'est uniquement un exemple pédagogique — ne l'utilisez pas en production. Préférez une phrase unique, longue (>16 caractères) et stockée dans un gestionnaire de mots de passe.

---

## 2) Démarrer l'agent SSH (option recommandée — nécessite élévation)

Ouvrez PowerShell en Administrateur puis exécutez :

```powershell
Set-Service -Name ssh-agent -StartupType Automatic
Start-Service ssh-agent
Get-Service ssh-agent
```

Si vous obtenez “Accès refusé”, relancez PowerShell en tant qu’administrateur ou utilisez une alternative (voir 2b).

### 2b) Alternatives si vous n'avez pas d'accès admin

- Git Bash : ouvrez Git Bash ; l'agent SSH y fonctionne souvent sans configuration système.
- Pageant (PuTTY) : convertir la clé en `.ppk` avec PuTTYgen puis charger dans Pageant.

---

## 3) Charger la clé privée dans l'agent (session utilisateur normale)

Après démarrage du service (ou dans Git Bash / Pageant selon l'alternative) :

```powershell
ssh-add $env:USERPROFILE\.ssh\id_ed25519
ssh-add -l
```

Vous saisissez la passphrase une seule fois ; `ssh-add -l` liste les clés chargées.

---

## 4) Copier la clé publique vers le serveur (commande exécutée localement)

Adaptez port/utilisateur/hôte si besoin :

```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh -p 2272 cyberlitech@192.168.1.250 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

Cette commande crée/ajoute `~/.ssh/authorized_keys` à distance.

---

## 5) Tester la connexion depuis le client

```powershell
ssh -p 2272 cyberlitech@192.168.1.250
```

Si tout est correct, la connexion se fera sans mot de passe (sauf si la passphrase doit être saisie parce que la clé n'est pas chargée dans l'agent).

---

## 6) Vérifications sur le serveur (Linux — distant)

Sur le serveur, corrigez permissions et propriétaire :

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chown -R cyberlitech:cyberlitech ~/.ssh
```

Vérifiez `sshd_config` (root) et rechargez si nécessaire :

```bash
sudo nano /etc/ssh/sshd_config   # vérifier PubkeyAuthentication yes, PasswordAuthentication no si souhaité
sudo systemctl reload sshd
```

### Configuration recommandée et restriction d'accès par réseau

Avant de remplacer ou vider `/etc/ssh/sshd_config`, sauvegardez le fichier existant et testez la syntaxe :

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
sudo sshd -t
```

Exemple de configuration prête à coller dans `/etc/ssh/sshd_config` (adapter le `Port` si nécessaire) :

```text
# Port d'écoute (adapter si non standard)
Port 2272

# Authentification
PermitRootLogin no
PubkeyAuthentication yes
PasswordAuthentication no
ChallengeResponseAuthentication no
PermitEmptyPasswords no

# Sécurité des fichiers et sessions
StrictModes yes
AllowAgentForwarding no
AllowTcpForwarding no
X11Forwarding no
MaxAuthTries 6
MaxSessions 4
LoginGraceTime 2m

# Options supplémentaires
UsePAM yes
ClientAliveInterval 300
ClientAliveCountMax 2

# NOTE: "Match" doit être placé en fin de fichier s'il est utilisé.
```

Remarque importante : sshd ne fournit pas une directive unique pour *refuser* toutes les sources sauf un réseau. La méthode fiable pour n'accepter que des connexions depuis des hôtes précis (par exemple `192.168.1.100` et `192.168.1.101`) est d'appliquer des règles au pare-feu du serveur (UFW ou iptables). Vous pouvez, en complément, ajouter des contrôles avec un bloc `Match` si vous avez des besoins spécifiques, mais le pare-feu est recommandé pour bloquer l'accès réseau.

Exemples de règles firewall :

- Avec `ufw` (déployer sur les distributions qui utilisent UFW) :

```bash
# Autoriser seulement 2 hôtes spécifiques avec UFW :
sudo ufw allow from 192.168.1.100 to any port 2272 proto tcp
sudo ufw allow from 192.168.1.101 to any port 2272 proto tcp
# Bloquer les autres adresses sur ce port (optionnel, selon règles UFW par défaut)
sudo ufw deny proto tcp to any port 2272
sudo ufw reload
```

Cette commande autorise exclusivement la plage `10.100.80.0/24` sur le port `2272`. Si vous n'utilisez pas UFW, utilisez `iptables` :

- Avec `iptables` (exemple immédiat, à persister selon votre distribution) :

```bash
# Autoriser seulement 2 hôtes spécifiques avec iptables :
sudo iptables -I INPUT -p tcp --dport 2272 -s 192.168.1.100 -j ACCEPT
sudo iptables -I INPUT -p tcp --dport 2272 -s 192.168.1.101 -j ACCEPT
# Refuser ensuite les autres connexions sur ce port
sudo iptables -A INPUT -p tcp --dport 2272 -j DROP

# Pour persister les règles sur Debian/Ubuntu :
sudo apt-get install -y iptables-persistent
sudo netfilter-persistent save
```

Vérifiez toujours, depuis une autre session, que vous pouvez toujours vous reconnecter avant de fermer votre session SSH administrateur ; en cas d'erreur, restaurez la sauvegarde :

```bash
sudo cp /etc/ssh/sshd_config.bak /etc/ssh/sshd_config
sudo systemctl reload sshd
```

Après modification, testez la configuration et rechargez `sshd` :

```bash
sudo sshd -t
sudo systemctl reload sshd
```

Si vous préférez une solution interne à `sshd`, vous pouvez ajouter un bloc `Match` en fin de fichier pour *adapter* le comportement selon l'adresse source, par exemple :

```text
# En fin de fichier :
Match Address 192.168.1.100,192.168.1.101
	# options spécifiques pour les clients de la plage
	PasswordAuthentication no
	PubkeyAuthentication yes
```

Mais attention : ce bloc ne bloque pas par lui-même les autres adresses — utilisez le pare-feu pour faire le filtrage réseau effectif.


---

## Schéma ASCII — Emplacement des clés (client Windows ↔ serveur Linux)

Client Windows (votre PC)                     Serveur Linux (hôte distant)

C:\Users\cyberlitech\.ssh\                        /home/cyberlitech/.ssh/

	+---------------------------+                 +---------------------------+
	| id_ed25519                |                 | (aucune clé privée ici)   |
	| (private key)             |                 |                           |
	+---------------------------+                 | authorized_keys (pub)     |
	| id_ed25519.pub            |  --copiée-->    |  contient la clé publique |
	+---------------------------+                 +---------------------------+

Explication :
- La clé privée (`id_ed25519`) reste sur le client Windows et n'est jamais transférée.
- La clé publique (`id_ed25519.pub`) est copiée dans `/home/cyberlitech/.ssh/authorized_keys` sur le serveur.
- L'agent SSH sur Windows stocke la clé privée en mémoire pour éviter de ressaisir la passphrase à chaque connexion.

---

## Remarques de sécurité

- Ne partagez jamais votre clé privée.
- La passphrase protège la clé privée sur le disque ; l'agent permet une saisie unique par session.
- Générer la paire sur le client et copier uniquement la clé publique est la bonne pratique.

---

Fichier créé pour usage pédagogique. Remplacez l'exemple de passphrase par une phrase secrète unique en environnement réel.


---

<div align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="440">
  </a>
</div>

<div align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</div>

