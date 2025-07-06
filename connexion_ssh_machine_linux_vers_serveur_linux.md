<!-- MASTER-HEADER-START -->
<div align="center">

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/headers/header-ssh.svg" alt="ATELIER SSH // BASTION & CRYPTOGRAPHIE" width="100%" />
</a>

<p align="center">
  <a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-portal.svg" alt="Portail 0xCyberLiTech.com" width="24%" /></a>
  <a href="https://0xcyberlitech.com/soc-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-soc-rd.svg" alt="Livre Blanc SOC Cockpit" width="24%" /></a>
  <a href="https://0xcyberlitech.com/jarvis-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-jarvis-rd.svg" alt="Livre Blanc JARVIS IA" width="24%" /></a>
  <a href="https://github.com/0xCyberLiTech?tab=repositories"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-github.svg" alt="Catalogue des 23 Dépôts" width="24%" /></a>
</p>
<p align="center">
  <a href="README.md"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-back-readme.svg" alt="Retour au sommaire du dépôt" width="340" /></a>
</p>

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />
</div>
<!-- MASTER-HEADER-END -->

<!-- DEBIAN-TRUTH-START -->
> [!IMPORTANT]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="18" height="18" align="absmiddle" alt="" /> ** Matrice Officielle Debian — `Debian 12 (Bookworm)` · `Debian 13 (Trixie)` · `Debian 14 (Forky)`**
> - **Sources Officielles Debian.org (`openssh`) :** `Bookworm (12)` : **`1:9.2p1-2+deb12u10`** &nbsp;·&nbsp; `Trixie (13 — Stable)` : **`1:10.0p1-7+deb13u4`** &nbsp;·&nbsp; `Forky (14 — Next-Gen)` : **`1:10.6p1-1`**
> - **Références Officielles :** [Paquet Debian Trixie (`openssh-server`)](https://packages.debian.org/trixie/openssh-server) &nbsp;·&nbsp; [Paquet Debian Forky (`openssh-server`)](https://packages.debian.org/forky/openssh-server) &nbsp;·&nbsp; [Documentation Officielle Debian](https://wiki.debian.org/SSH)
> - **Note d'Ingénierie (Divergence 13 vs 14) :** Sous Debian 13 (Trixie) et Debian 14 (Forky), l'unité systemd se nomme **`ssh.service`** (et non `sshd`), les surcharges se placent dans **`/etc/ssh/sshd_config.d/*.conf`**, et les logs d'authentification se lisent via `journalctl -u ssh` (`/var/log/auth.log` n'existe plus sans `rsyslog`).

<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Afficher les Encarts Ligne de Commande : Debian 13 (Trixie — Stable) vs Debian 14 (Forky — Next-Gen)</b></summary>

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Profil Production Stable — Commandes pour `Debian 13 (Trixie)`
```bash
# Debian 13 (Trixie — OpenSSH 9.9+) : Durcissement modulaire dans /etc/ssh/sshd_config.d/
sudo sshd -t && sudo systemctl reload ssh
sudo journalctl -u ssh.service -n 50 --no-hostname
```

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-rd.svg" width="46" height="16" align="absmiddle" alt="[R&D]" /> Profil Anticipation Next-Gen — Commandes pour `Debian 14 (Forky)`
```bash
# Debian 14 (Forky — OpenSSH 10.x) : Suppression definitive du support DSA & echange post-quantique sntrup761/mlkem768
ssh -Q kex | grep -E 'mlkem|sntrup'
sudo sshd -T | grep -E 'permitrootlogin|passwordauthentication|port'
```

</details>
<!-- DEBIAN-TRUTH-END -->

<!-- CIEL-PEDAGOGY-START -->
<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Synthèse d'Architecture, Standards Officiels &amp; Diagnostic (Niveau 1 : Fondamentaux · Niveau 2 : Repères · Niveau 3 : Diagnostic)</b></summary>

- **Niveau 1 — Fondamentaux &amp; Principe d'Architecture :** **OpenSSH (`sshd`)** fournit un canal d'administration distante, d'exécution de commandes et de transfert de fichiers (`SFTP`) intégralement chiffré et authentifié de bout en bout.
- **Niveau 2 — Repères Officiels (Ports IANA, Fichiers Debian &amp; Commandes de Validation) :** **Port IANA :** `TCP 22` (ou port durci dédié) &nbsp;|&nbsp; **Fichiers Debian :** `/etc/ssh/sshd_config`, `/etc/ssh/sshd_config.d/*.conf`, `~/.ssh/authorized_keys` (`chmod 600`) &nbsp;|&nbsp; **Validation officielle :** `sudo sshd -t`.
- **Niveau 3 — Diagnostic d'Incidents &amp; Ingénierie Avancée :** **Diagnostic & Architecture :** Si l'authentification par clé publique échoue, contrôlez les droits POSIX stricts (`chmod 700 ~/.ssh` et `chmod 600 ~/.ssh/authorized_keys`). Désactivez l'authentification par mot de passe (`PasswordAuthentication no`) au profit de clés asymétriques `Ed25519`, de certificats SSH (CA) et de l'échange de clés hybride post-quantique (`mlkem768x25519-sha256` dès OpenSSH 9.9/10.0).
- **Sources de Vérité Officielles Éditeurs &amp; Standards :** [Manpage Officielle OpenSSH sshd_config(5)](https://man.openbsd.org/sshd_config) &nbsp;·&nbsp; [Spécifications Officielles OpenSSH](https://www.openssh.com/specs.html) &nbsp;·&nbsp; [Recommandations ANSSI OpenSSH](https://cyber.gouv.fr/)

</details>
<!-- CIEL-PEDAGOGY-END -->


# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> Connexion SSH par clés asymétriques d'un poste Linux (Debian) vers un serveur Debian

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 01 // TOPOLOGIE DU LAB & PRÉREQUIS
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

| Équipement | Rôle dans l'Atelier | Système d'Exploitation | Adresse IP de Lab |
|:---|:---|:---|:---|
| **Poste Client (`client-debian`)** | Machine d'administration générant la paire de clés | Debian 12 (`Bookworm`) / Debian 13 (`Trixie`) / Debian 14 (`Forky`) | `10.10.10.101` |
| **Serveur Cible (`srv-debian`)** | Serveur distant recevant la clé publique dans `authorized_keys` | Debian 12 (`Bookworm`) / Debian 13 (`Trixie`) / Debian 14 (`Forky`) | `10.10.10.102` (Port `2272`) |

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 02 // GÉNÉRATION DE LA PAIRE DE CLÉS CRYPTOGRAPHIQUES (`SSH-KEYGEN`)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> A. Recommandation Souveraine Debian 13 (Trixie) & Debian 14 (Forky) : Courbe Elliptique `Ed25519`

Depuis **OpenSSH 9.6+** (embarqué dans **Debian 13 `Trixie`** et **Debian 14 `Forky`**), l'algorithme par défaut de `ssh-keygen` est désormais **`Ed25519`** (plus rapide, empreinte compacte et résistance accrue aux attaques par canal auxiliaire). Sur **Debian 12 (`Bookworm`)** comme sur **Debian 13/14**, il est recommandé d'expliciter `-t ed25519 -a 100` (100 rondes de dérivation KDF `bcrypt` pour protéger la phrase de passe) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> ssh-keygen -t ed25519 -a 100 -C "admin@client-debian"
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> B. Alternative Compatible Systèmes Hérités : `RSA 4096 bits`

Si vous devez interagir avec des équipements anciens ne supportant pas `Ed25519`, générez une clé `RSA` d'au moins **4096 bits** :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> ssh-keygen -t rsa -b 4096 -a 100 -C "admin@client-debian"
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> C. Emplacement des Clés et Phrase de Passe (`Passphrase`)

Lors de l'exécution, `ssh-keygen` affiche l'invite suivante :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> Generating public/private ed25519 key pair.
> Enter file in which to save the key (/home/username/.ssh/id_ed25519):
> Created directory '/home/username/.ssh'.
> Enter passphrase (empty for no passphrase):
> Enter same passphrase again:
> ```
<!-- CODE-WINDOW-END -->

> [!TIP]
> **Pourquoi protéger votre clé privée par une phrase de passe (`Passphrase`) ?**
> - **Zéro exposition réseau :** La clé privée (`~/.ssh/id_ed25519`) ne quitte **jamais** votre machine cliente. La phrase de passe sert uniquement à déchiffrer la clé localement en mémoire vive (`ssh-agent`).
> - **Défense en profondeur :** Si un attaquant compromet votre poste client, la clé privée reste inutilisable sans la phrase de passe (chiffrée avec 100 rondes KDF `bcrypt`), vous laissant le temps de révoquer la clé publique sur vos serveurs.

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> D. Vérification des Fichiers Générés dans `~/.ssh`

Après la génération, vérifiez la présence de votre couple de clés (`id_ed25519` = clé privée secrète ; `id_ed25519.pub` = clé publique à déployer) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> ls -la ~/.ssh/
> # -rw------- 1 username username 464 nov. 01 10:00 id_ed25519
> # -rw-r--r-- 1 username username 102 nov. 01 10:00 id_ed25519.pub
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 03 // DÉPLOIEMENT DE LA CLÉ PUBLIQUE SUR LE SERVEUR DISTANT (`SSH-COPY-ID`)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Transférez votre clé publique (`~/.ssh/id_ed25519.pub`) vers le serveur Debian distant (`10.10.10.102`, port personnalisé `2272`) à l'aide de l'utilitaire officiel `ssh-copy-id` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> ssh-copy-id -i ~/.ssh/id_ed25519.pub -p 2272 root@10.10.10.102
> ```
<!-- CODE-WINDOW-END -->

Une dernière authentification par mot de passe vous est demandée afin d'inscrire automatiquement votre clé publique dans `/root/.ssh/authorized_keys` sur le serveur distant.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 04 // CONTRÔLE DES PERMISSIONS & TEST D'AUTHENTIFICATION PAR CLÉ
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> A. Connexion et Verrouillage Stricte des Permissions (`chmod 700 / 600`)

Connectez-vous au serveur distant et vérifiez que les permissions POSIX du dossier `.ssh` (`700`) et du fichier `authorized_keys` (`600`) sont strictement verrouillées (OpenSSH refusera l'authentification par clé si le mode `StrictModes yes` détecte des permissions trop larges) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> ssh -p 2272 root@10.10.10.102
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> chmod 700 ~/.ssh
> chmod 600 ~/.ssh/authorized_keys
> ls -ld ~/.ssh ~/.ssh/authorized_keys
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> B. Validation de la Connexion Transparente depuis le Poste Client

Depuis votre poste client (`10.10.10.101`), testez la connexion par clé :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> ssh -i ~/.ssh/id_ed25519 -p 2272 root@10.10.10.102
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 05 // DURCISSEMENT DU SERVEUR OPENSSH (`DEBIAN 12` · `DEBIAN 13 TRIXIE` · `DEBIAN 14 FORKY`)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> A. Configuration Modulaire Recommandée (`/etc/ssh/sshd_config.d/99-hardening.conf`)

Sous **Debian 12 (`Bookworm`)**, **Debian 13 (`Trixie`)** et **Debian 14 (`Forky`)**, le fichier `/etc/ssh/sshd_config` inclut automatiquement `Include /etc/ssh/sshd_config.d/*.conf`.
Plutôt que d'altérer le fichier maître (ce qui provoque des conflits lors des mises à jour `apt upgrade`), créez un fichier de durcissement dédié `/etc/ssh/sshd_config.d/99-hardening.conf` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```ini
> # /etc/ssh/sshd_config.d/99-hardening.conf — Durcissement Bastion SSH Debian 12 / 13 (Trixie) / 14 (Forky)
> Port 2272
> LoginGraceTime 1m
> PermitRootLogin prohibit-password
> StrictModes yes
> MaxAuthTries 4
> MaxSessions 2
>
> PubkeyAuthentication yes
> PasswordAuthentication no
> KbdInteractiveAuthentication no
> PermitEmptyPasswords no
> X11Forwarding no
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> B. Validation Syntaxique (`sshd -t`) et Rechargement Sans Coupure

Avant tout redémarrage du démon SSH à distance, validez **impérativement** la syntaxe avec `sshd -t`, puis rechargez le service `ssh.service` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo sshd -t && sudo systemctl reload ssh.service
> sudo systemctl status ssh.service --no-pager
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> C. Consultation des Journaux d'Authentification (`Debian 13 Trixie` & `Debian 14 Forky`)

Sous **Debian 13 (`Trixie`)** et **Debian 14 (`Forky`)**, `rsyslog` (`/var/log/auth.log`) n'est plus installé par défaut : interrogez directement le journal binaire `systemd-journald` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo journalctl -u ssh.service -n 30 --no-hostname
> ```
<!-- CODE-WINDOW-END -->

<!-- MASTER-FOOTER-START -->
<div align="center">
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/footer-master.svg" alt="0xCyberLiTech — Architecture Cyberdéfense, Ingénierie Déterministe & IA Souveraine" width="100%" />
</a>

<p align="center"><a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/badge-antigravity.svg" alt="Architecturé par Marc & Antigravity (Google DeepMind)" width="520" /></a></p>

<sub><b>Architecturé &amp; Forgé par Marc &amp; Antigravity (Google DeepMind)</b> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/"><b>0xcyberlitech.com</b></a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/soc-rd.html">Architecture SOC Cockpit v5.5</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/jarvis-rd.html">Architecture JARVIS Mark-VII</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/blueprint-jarvis.html">Blueprint Matériel RTX 5080</a></sub>

</div>
<!-- MASTER-FOOTER-END -->
