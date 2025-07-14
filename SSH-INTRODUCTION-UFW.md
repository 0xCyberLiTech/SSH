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

# 🔥 Configurer un pare‑feu local avec **UFW** sur **Debian 12**

---

## 1. Pourquoi un pare‑feu ?
Un pare‑feu limite l’exposition d’un serveur :
- **Filtrage entrant** : seuls les services voulus sont accessibles.
- **Filtrage sortant** : la machine ne parle qu’aux destinations autorisées (utile contre l’exfiltration).
- **Journalisation** : traçabilité des tentatives d’accès.

---

## 2. Installation et premiers réglages
```bash
sudo apt update && sudo apt install ufw -y
```
> ⚠️ **Toujours** disposer d’un accès console (KVM/virtuel ou physique) avant d’activer un pare‑feu, au cas où la connexion SSH se verrouille.

### 2.1 – Activer IPv6
UFW gère IPv6. Vérifie que `IPV6=yes` dans `/etc/default/ufw` puis :
```bash
sudo ufw reload
```

### 2.2 – Définir les politiques par défaut (stratégie « deny by default »)
```bash
sudo ufw default deny incoming   # tout trafic entrant bloqué
sudo ufw default allow outgoing  # tout trafic sortant autorisé
```
> 👉 Inverse **allow ↔ deny** si tu veux une machine _cloisonnée_ même en sortie.

### 2.3 – Autoriser le SSH avant d’activer le pare‑feu
```bash
# Port standard
sudo ufw allow 22/tcp
# Ou port personnalisé (ex : 2266)
sudo ufw allow 2266/tcp
```

### 2.4 – Activation
```bash
sudo ufw enable   # répondre y
```
Le pare‑feu se lancera automatiquement au démarrage (`systemctl status ufw`).

---

## 3. Commandes essentielles
### 3.1 – Lister les règles
```bash
sudo ufw status numbered    # affichage compact avec numéros
sudo ufw status verbose     # détails + IPv6 + policies
```

### 3.2 – Autoriser des flux
| Cas d’usage | Commande |
|-------------|----------|
| Autoriser **HTTP/HTTPS** | `sudo ufw allow 80,443/tcp` |
| Autoriser **FTP passif (1024‑1048)** | `sudo ufw allow 1024:1048/tcp` |
| Autoriser **un sous‑réseau** | `sudo ufw allow from 10.10.0.0/24 to any port 22 proto tcp` |
| Autoriser **une IP** | `sudo ufw allow from 203.0.113.42 to any port 54321 proto tcp` |

### 3.3 – Bloquer des flux
```bash
# Bloquer une IP source\sudo ufw deny from 203.0.113.66

# Bloquer tout trafic sortant vers le port 25 (anti‑spam)
sudo ufw deny out 25/tcp
```

### 3.4 – Supprimer / réinitialiser
```bash
sudo ufw delete <numéro>   # après ufw status numbered
sudo ufw reset             # RAZ totale (demande confirmation)
```

### 3.5 – Profils applicatifs
```bash
sudo ufw app list              # voir la liste
sudo ufw app info "Samba"       # détails (ports, proto)
sudo ufw allow "Nginx Full"     # ouvre 80 + 443
```
Les profils sont stockés dans `/etc/ufw/applications.d/`.

---

## 4. Exemples pratiques (scénarios)
### 4.1 – Serveur web + SSH restreint
```bash
sudo ufw reset
sudo ufw default deny incoming
sudo ufw default allow outgoing
# SSH uniquement depuis IP admin
sudo ufw allow from 198.51.100.5 to any port 2266 proto tcp
# HTTP / HTTPS publics
sudo ufw allow 80,443/tcp
sudo ufw enable
```

### 4.2 – Limiter le brute‑force SSH (rate limiting)
```bash
# Autorise 10 nouvelles connexions par 30 s (IPv4 + IPv6)
sudo ufw limit 22/tcp comment "Anti brute‑force"
```

### 4.3 – Bloquer tout sauf mises à jour APT sortantes
```bash
sudo ufw reset
sudo ufw default deny incoming
sudo ufw default deny outgoing
# DNS pour resolve
sudo ufw allow out 53/udp
# HTTP/HTTPS vers miroirs Debian
sudo ufw allow out 80,443/tcp
sudo ufw enable
```

---

## 5. Fichiers internes & interaction avec iptables
| Fichier | Rôle |
|---------|------|
| `/etc/ufw/user.rules` | convertit tes commandes en règles iptables (IPv4) |
| `/etc/ufw/user6.rules` | idem pour IPv6 |
| `/etc/ufw/before.rules` | règles évaluées **avant** celles de l’utilisateur (ex : ICMP) |
| `/etc/ufw/after.rules`  | règles évaluées **après** |

✏️ Exemple : pour bloquer le ping sur tout le système, édite *before.rules* et remplace les 4 règles ICMP `ACCEPT` par `DROP`, puis `sudo ufw reload`.

---

## 6. Journalisation (logs)
```bash
sudo ufw logging medium   # low | medium | high
# logs : /var/log/ufw.log (rsyslog) ou journalctl -u ufw
```

- **low** : connexions bloquées seulement.
- **medium** : + connexions autorisées.
- **high** : détails des paquets (verbeux).

---

## 7. Sauvegarde et restauration manuelle
```bash
sudo ufw export > ufw-backup.conf   # exporte les règles
sudo ufw import ufw-backup.conf     # restaure
```

---

## 8. Désactivation temporaire
```bash
sudo ufw disable       # stoppe le pare‑feu
sudo ufw enable        # ré‑active
```

---

## 9. Bonnes pratiques
- **Appliquer la stratégie « deny by default »** et n’ouvrir que ce qui est nécessaire.
- **Limiter** les services exposés (SSH => port personnalisé + `ufw limit`).
- Surveiller `ufw.log` pour ajuster les règles.
- Sauvegarder la configuration après chaque modification majeure.
- Tester depuis une deuxième session SSH avant `ufw enable`.

---

> 📝 *Dernière mise à jour : 14 juillet 2025*



---

<p align="center">
  🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessible à tous.
</p>

