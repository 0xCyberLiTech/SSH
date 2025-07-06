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
> [!TIP]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> **Guide de Lecture &amp; Progression par Niveau (SSH)**
> - **Rôle de la brique :** **OpenSSH (`sshd`)** fournit un canal d'administration distante, d'exécution de commandes et de transfert de fichiers (`SFTP`) intégralement chiffré et authentifié de bout en bout.
> - **Parcours recommandé :** **Niveau 1 (Fondamentaux &amp; Installation initiale)** pour déployer une base saine &rarr; **Niveau 2 (Configuration &amp; Intégration)** &rarr; **Niveau 3 (Haute Disponibilité, Durcissement &amp; Exploitation)**.

<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Synthèse d'Architecture, Standards Officiels &amp; Diagnostic (Niveau 1 : Fondamentaux · Niveau 2 : Repères · Niveau 3 : Diagnostic)</b></summary>

- **Niveau 1 — Fondamentaux &amp; Principe d'Architecture :** **OpenSSH (`sshd`)** fournit un canal d'administration distante, d'exécution de commandes et de transfert de fichiers (`SFTP`) intégralement chiffré et authentifié de bout en bout.
- **Niveau 2 — Repères Officiels (Ports IANA, Fichiers Debian &amp; Commandes de Validation) :** **Port IANA :** `TCP 22` (ou port durci dédié) &nbsp;|&nbsp; **Fichiers Debian :** `/etc/ssh/sshd_config`, `/etc/ssh/sshd_config.d/*.conf`, `~/.ssh/authorized_keys` (`chmod 600`) &nbsp;|&nbsp; **Validation officielle :** `sudo sshd -t`.
- **Niveau 3 — Diagnostic d'Incidents &amp; Ingénierie Avancée :** **Diagnostic & Architecture :** Si l'authentification par clé publique échoue, contrôlez les droits POSIX stricts (`chmod 700 ~/.ssh` et `chmod 600 ~/.ssh/authorized_keys`). Désactivez l'authentification par mot de passe (`PasswordAuthentication no`) au profit de clés asymétriques `Ed25519`, de certificats SSH (CA) et de l'échange de clés hybride post-quantique (`mlkem768x25519-sha256` dès OpenSSH 9.9/10.0).
- **Sources de Vérité Officielles Éditeurs &amp; Standards :** [Manpage Officielle OpenSSH sshd_config(5)](https://man.openbsd.org/sshd_config) &nbsp;·&nbsp; [Spécifications Officielles OpenSSH](https://www.openssh.com/specs.html) &nbsp;·&nbsp; [Recommandations ANSSI OpenSSH](https://cyber.gouv.fr/)

</details>
<!-- CIEL-PEDAGOGY-END -->


## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 01 // SOMMAIRE DES DOSSIERS TECHNIQUES — ATELIER SSH // BASTION & CRYPTOGRAPHIE
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<div align="center">

| Catégorie | Sujet                              | Accès Rapide                                                                                                                                                |
|-----------|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **SSH**   | Connexion SSH — Windows (PowerShell) → Serveur Linux. | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](connexion_ssh_windows_powershell_vers_serveur_linux.md) |
| **SSH**   | Connexion SSH — Machine Linux (Debian) → Serveur Linux (DEBIAN). | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](connexion_ssh_machine_linux_vers_serveur_linux.md) |
| **SSH** | Durcissement OpenSSH 9.9/10.0 : Cryptographie Post-Quantique (ML-KEM), Autorité de Certification SSH & FIDO2 sur Debian 12, 13 & 14 | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](SSH-POST-QUANTIQUE-CA-FIDO2-DEBIAN-13-14.md) |

</div>

---

# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> Le protocole SSH

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 02 // Qu’est-ce que SSH ?
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

**SSH** (Secure Shell) est un protocole réseau permettant d'établir une connexion sécurisée entre un client et un serveur, principalement pour administrer des systèmes à distance.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 03 // Objectifs principaux de SSH :
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- **Sécurité** : chiffrer toutes les communications pour éviter l’espionnage.
- **Authentification** : vérifier l’identité du client (et parfois du serveur).
- **Intégrité** : garantir que les données échangées ne sont pas altérées.
- **Confidentialité** : empêcher les interceptions et accès non autorisés.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 04 // Comment fonctionne SSH ?
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

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

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 05 // Les avantages de SSH :
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- **Sécurité renforcée** par rapport à des protocoles comme Telnet (non chiffré).
- **Multiples usages** : administration distante, transfert de fichiers (SCP, SFTP), tunnels sécurisés.
- **Authentification par clé publique** qui supprime le besoin de mot de passe.
- **Support sur tous les systèmes Unix/Linux** et sur Windows avec des clients compatibles.

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
