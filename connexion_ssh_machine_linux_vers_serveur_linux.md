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

# Connexion SSH depuis une machine linux (Debian) vers un serveur linux (Debian).

machine linux local 10.10.10.101
serveur linux distant 10.10.10.102

Pour commencer, nous allons générer une paire de clés SSH à l’aide de la commande ssh-keygen.

Effectuez cette opération depuis la machine (Linux Debian) qui servira à se connecter à votre serveur distant (également sous Linux Debian) :

```bash
ssh-keygen
```

Si aucune option n’est spécifiée, une clé RSA de 2048 bits sera créée, ce qui reste acceptable aujourd’hui en termes de sécurité.

Pour générer une clé de taille différente, utilisez l’option -b :

```bash
ssh-keygen -b 4096
```

Generating public/private rsa key pair.
Enter file in which to save the key (/home/username/.ssh/id_rsa):

L’utilitaire vous demandera de sélectionner un emplacement pour les clés qui seront générées.

Le système stockera les clés par défaut dans le répertoire ~/.ssh du répertoire d’accueil de votre utilisateur. La clé privée se nommera id_rsa et la clé publique associée, id_rsa.pub.

/root/.ssh pour l’utilisateur root).

ou

/username/.ssh pour l’utilisateur username).

En règle générale, à ce stade, il est préférable de conserver l’emplacement par défaut. Cela permettra à votre client SSH de trouver automatiquement vos clés SSH lorsqu’il voudra s’authentifier. Si vous souhaitez choisir un autre chemin, vous devez le saisir maintenant. Sinon, appuyez sur ENTER pour accepter l’emplacement par défaut.

Si vous avez précédemment généré une paire de clés SSH, vous verrez apparaître une invite similaire à la suivante :

```
/home/username/.ssh/id_rsa already exists.
Overwrite (y/n)?
```

Si vous choisissez d’écraser la clé sur le disque, vous ne pourrez plus vous authentifier à l’aide de la clé précédente. Soyez très prudent lorsque vous sélectionnez « yes », car il s’agit d’un processus de suppression irréversible.

Created directory '/home/username/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:

Vous serez ensuite invité à saisir une phrase de passe pour la clé. Il s’agit d’une phrase de passe facultative qui peut servir à crypter le fichier de la clé privée sur le disque.

Il serait légitime de vous demander quels avantages pourrait avoir une clé SSH si vous devez tout de même saisir une phrase de passe.

Voici quelques-uns des avantages :

La clé SSH privée (la partie qui peut être protégée par une phrase de passe) n’est jamais exposée sur le réseau. La phrase de passe sert uniquement à décrypter la clé sur la machine locale. Cela signifie que toute attaque par force brute du réseau sera impossible avec une phrase de passe.

La clé privée est conservée dans un répertoire à accès restreint. Le client SSH ne pourra pas reconnaître des clés privées qui ne sont pas conservées dans des répertoires à accès restreint. La clé elle-même doit également être configurée avec des autorisations restreintes (lecture et écriture uniquement disponibles pour le propriétaire). Cela signifie que les autres utilisateurs du système ne peuvent pas vous espionner.

Tout attaquant souhaitant craquer la phrase de passe de la clé SSH privée devra préalablement avoir accès au système. Ce qui signifie qu’il aura déjà accès à votre compte utilisateur ou le compte root. Dans ce genre de situation, la phrase de passe peut empêcher l’attaquant de se connecter immédiatement à vos autres serveurs, en espérant que cela vous donne du temps pour créer et implémenter une nouvelle paire de clés SSH et supprimer l’accès de la clé compromise.

Étant donné que la clé privée n’est jamais exposée au réseau et est protégée par des autorisations d’accès au fichier, ce fichier ne doit jamais être accessible à toute autre personne que vous (et le root user). La phrase de passe offre une couche de protection supplémentaire dans le cas où ces conditions seraient compromises.

L’ajout d’une phrase de passe est facultatif. Si vous en entrez une, vous devrez la saisir à chaque fois que vous utiliserez cette clé (à moins que vous utilisiez un logiciel d’agent SSH qui stocke la clé décryptée). Nous vous recommandons d’utiliser une phrase de passe. Cependant, si vous ne souhaitez pas définir une phrase de passe, il vous suffit d’appuyer sur ENTER pour contourner cette invite.

Après la création, vous trouverez vos clés dans le répertoire ~/.ssh :

~/.ssh/id_xxx : votre clé privée
~/.ssh/id_xxx.pub : votre clé publique

Pour vérifier la présence des fichiers :

```bash
cd ~/.ssh
ls 
id_ed25519
id_ed25519.pub
```

Transférer la clé publique vers le serveur distant
Transférez maintenant la clé publique (id_ed25519.pub) vers votre serveur distant, depuis votre machine locale.

Exemple avec l’IP du serveur distant : 10.10.10.102 :

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub -p 2272 root@10.10.10.102
```

Une authentification vous sera demandée.

Cette commande va copier votre clé publique sur le serveur distant, dans le fichier authorized_keys du dossier ~/.ssh de la session distante (ici, root).

Vérifier et sécuriser les droits d’accès

Connectez-vous ensuite en SSH au serveur distant :

```bash
ssh -p 2272 root@10.10.10.102
```

Sécurisez le dossier ~/.ssh/ et le fichier authorized_keys :

```bash
cd /root/
chmod 700 .ssh/
cd /root/.ssh/
chmod 600 authorized_keys
```

Redémarrez le service SSH :

```bash
systemctl restart ssh.service
```

Vous pouvez désormais vous connecter depuis la machine locale vers le serveur distant en utilisant cette clé publique :

```bash
ssh -p 2272 root@10.10.10.102
```

L’authentification est maintenant transparente grâce à la clé publique déposée au préalable.

Modifier la configuration SSH

Il est recommandé de modifier la configuration du fichier /etc/ssh/sshd_config pour renforcer la sécurité.

Exemple de configuration à adapter (notamment le port si besoin) :

```conf
# Authentication:

LoginGraceTime 1m
#PermitRootLogin prohibit-password
PermitRootLogin yes
#StrictModes yes
MaxAuthTries 4
MaxSessions 2

PubkeyAuthentication yes

# To disable tunneled clear text passwords, change to "no" here!
PasswordAuthentication no

PasswordAuthentication no # Vous ne pourrez plus vous connecter en ssh via votre login et password
```

---

<div align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="440">
  </a>
</div>

<div align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</div>
