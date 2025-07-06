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


# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> Connexion SSH - Windows (PowerShell) → Serveur Linux

But : Générer une paire ed25519 sur le client Windows, charger la clé privée dans l'agent (passphrase saisie une seule fois), copier la clé publique sur le serveur et tester la connexion.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 01 // 1) Générer la paire (PowerShell)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Exécutez dans PowerShell (session utilisateur) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```powershell
> ssh-keygen -t ed25519 -C "srv-linux" -f "$env:USERPROFILE\.ssh\id_ed25519"
> ```
<!-- CODE-WINDOW-END -->

Quand on vous demande une passphrase, pour l'exemple pédagogique utilisez :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> Jesuisenweekenddans6h00cestsuper
> ```
<!-- CODE-WINDOW-END -->

Remarque : c'est uniquement un exemple pédagogique — ne l'utilisez pas en production. Préférez une phrase unique, longue (>16 caractères) et stockée dans un gestionnaire de mots de passe.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 02 // 2) Démarrer l'agent SSH (option recommandée — nécessite élévation)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Ouvrez PowerShell en Administrateur puis exécutez :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```powershell
> Set-Service -Name ssh-agent -StartupType Automatic
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```powershell
> Start-Service ssh-agent
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```powershell
> Get-Service ssh-agent
> ```
<!-- CODE-WINDOW-END -->

Si vous obtenez “Accès refusé”, relancez PowerShell en tant qu’administrateur ou utilisez une alternative (voir 2b).

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> 2b) Alternatives si vous n'avez pas d'accès admin

- Git Bash : ouvrez Git Bash ; l'agent SSH y fonctionne souvent sans configuration système.
- Pageant (PuTTY) : convertir la clé en `.ppk` avec PuTTYgen puis charger dans Pageant.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 03 // 3) Charger la clé privée dans l'agent (session utilisateur normale)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Après démarrage du service (ou dans Git Bash / Pageant selon l'alternative) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```powershell
> ssh-add $env:USERPROFILE\.ssh\id_ed25519
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```powershell
> ssh-add -l
> ```
<!-- CODE-WINDOW-END -->

Vous saisissez la passphrase une seule fois ; `ssh-add -l` liste les clés chargées.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 04 // 4) Copier la clé publique vers le serveur (commande exécutée localement)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Adaptez port/utilisateur/hôte si besoin :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```powershell
> type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh -p 2272 username@192.168.1.250 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
> ```
<!-- CODE-WINDOW-END -->

Cette commande crée/ajoute `~/.ssh/authorized_keys` à distance.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 05 // 5) Tester la connexion depuis le client
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```powershell
> ssh -p 2272 username@192.168.1.250
> ```
<!-- CODE-WINDOW-END -->

Si tout est correct, la connexion se fera sans mot de passe (sauf si la passphrase doit être saisie parce que la clé n'est pas chargée dans l'agent).

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 06 // 6) Vérifications sur le serveur (Linux — distant)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Sur le serveur, corrigez permissions et propriétaire :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> chmod 700 ~/.ssh
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> chmod 600 ~/.ssh/authorized_keys
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> chown -R username:username ~/.ssh
> ```
<!-- CODE-WINDOW-END -->

Vérifiez `sshd_config` (root) et rechargez si nécessaire :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```ini
> sudo nano /etc/ssh/sshd_config   # vérifier PubkeyAuthentication yes, PasswordAuthentication no si souhaité
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl reload ssh
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Configuration recommandée et restriction d'accès par réseau

Avant de remplacer ou vider `/etc/ssh/sshd_config`, sauvegardez le fichier existant et testez la syntaxe :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo sshd -t
> ```
<!-- CODE-WINDOW-END -->

Exemple de configuration prête à coller dans `/etc/ssh/sshd_config` (adapter le `Port` si nécessaire) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```ini
> # Port d'écoute (adapter si non standard)
> Port 2272
>
> # Authentification
> PermitRootLogin no
> PubkeyAuthentication yes
> PasswordAuthentication no
> ChallengeResponseAuthentication no
> PermitEmptyPasswords no
>
> # Sécurité des fichiers et sessions
> StrictModes yes
> AllowAgentForwarding no
> AllowTcpForwarding no
> X11Forwarding no
> MaxAuthTries 6
> MaxSessions 4
> LoginGraceTime 2m
>
> # Options supplémentaires
> UsePAM yes
> ClientAliveInterval 300
> ClientAliveCountMax 2
>
> # NOTE: "Match" doit être placé en fin de fichier s'il est utilisé.
> ```
<!-- CODE-WINDOW-END -->

Remarque importante : sshd ne fournit pas une directive unique pour *refuser* toutes les sources sauf un réseau. La méthode fiable pour n'accepter que des connexions depuis des hôtes précis (par exemple `192.168.1.100` et `192.168.1.101`) est d'appliquer des règles au pare-feu du serveur (UFW ou iptables). Vous pouvez, en complément, ajouter des contrôles avec un bloc `Match` si vous avez des besoins spécifiques, mais le pare-feu est recommandé pour bloquer l'accès réseau.

Exemples de règles firewall :

- Avec `ufw` (déployer sur les distributions qui utilisent UFW) :

# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> Autoriser seulement 2 hôtes spécifiques avec UFW :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw allow from 192.168.1.100 to any port 2272 proto tcp
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw allow from 192.168.1.101 to any port 2272 proto tcp
> ```
<!-- CODE-WINDOW-END -->

# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> Bloquer les autres adresses sur ce port (optionnel, selon règles UFW par défaut)

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw deny proto tcp to any port 2272
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw reload
> ```
<!-- CODE-WINDOW-END -->

Cette commande autorise exclusivement la plage `10.100.80.0/24` sur le port `2272`. Si vous n'utilisez pas UFW, utilisez `iptables` :

- Avec `iptables` (exemple immédiat, à persister selon votre distribution) :

# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> Autoriser seulement 2 hôtes spécifiques avec iptables :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -I INPUT -p tcp --dport 2272 -s 192.168.1.100 -j ACCEPT
> sudo iptables -I INPUT -p tcp --dport 2272 -s 192.168.1.101 -j ACCEPT
> ```
<!-- CODE-WINDOW-END -->

# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> Refuser ensuite les autres connexions sur ce port

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -A INPUT -p tcp --dport 2272 -j DROP
> ```
<!-- CODE-WINDOW-END -->

# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> Pour persister les règles sur Debian/Ubuntu :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt-get install -y iptables-persistent
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo netfilter-persistent save
> ```
<!-- CODE-WINDOW-END -->

Vérifiez toujours, depuis une autre session, que vous pouvez toujours vous reconnecter avant de fermer votre session SSH administrateur ; en cas d'erreur, restaurez la sauvegarde :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo cp /etc/ssh/sshd_config.bak /etc/ssh/sshd_config
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl reload ssh
> ```
<!-- CODE-WINDOW-END -->

Après modification, testez la configuration et rechargez `sshd` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo sshd -t
> ```
<!-- CODE-WINDOW-END -->

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl reload ssh
> ```
<!-- CODE-WINDOW-END -->

Si vous préférez une solution interne à `sshd`, vous pouvez ajouter un bloc `Match` en fin de fichier pour *adapter* le comportement selon l'adresse source, par exemple :

# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> En fin de fichier :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```ini
> Match Address 192.168.1.100,192.168.1.101
> 	# options spécifiques pour les clients de la plage
> 	PasswordAuthentication no
> 	PubkeyAuthentication yes
> ```
<!-- CODE-WINDOW-END -->

Mais attention : ce bloc ne bloque pas par lui-même les autres adresses — utilisez le pare-feu pour faire le filtrage réseau effectif.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 07 // Schéma ASCII — Emplacement des clés (client Windows ↔ serveur Linux)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> Client Windows (votre PC)                     Serveur Linux (hote distant)
> C:\Users\username\.ssh\                       /home/username/.ssh/
>
> +---------------------------+                 +---------------------------+
> | id_ed25519                |                 | (aucune cle privee ici)   |
> | (private key)             |                 |                           |
> +---------------------------+                 | authorized_keys (pub)     |
> | id_ed25519.pub            |  --copiee-->    |  contient la cle publique |
> +---------------------------+                 +---------------------------+
> ```
<!-- CODE-WINDOW-END -->

Explication :
- La clé privée (`id_ed25519`) reste sur le client Windows et n'est jamais transférée.
- La clé publique (`id_ed25519.pub`) est copiée dans `/home/username/.ssh/authorized_keys` sur le serveur.
- L'agent SSH sur Windows stocke la clé privée en mémoire pour éviter de ressaisir la passphrase à chaque connexion.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 08 // Remarques de sécurité
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- Ne partagez jamais votre clé privée.
- La passphrase protège la clé privée sur le disque ; l'agent permet une saisie unique par session.
- Générer la paire sur le client et copier uniquement la clé publique est la bonne pratique.

---

Fichier créé pour usage pédagogique. Remplacez l'exemple de passphrase par une phrase secrète unique en environnement réel.


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
