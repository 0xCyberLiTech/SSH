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

# 🔒 Résumé Complet : `iptables` pour la Sécurité Linux

---

## 🔗 Qu'est-ce que `iptables` ?

`iptables` est un outil en ligne de commande sous Linux qui permet de :
- Contrôler le trafic réseau entrant, sortant et transitant.
- Appliquer des règles de sécurité sur les connexions.
- Créer un pare-feu robuste adapté aux besoins de l'administrateur.

---

## 🛠️ Structure de base

```bash
iptables -A [chaîne] [filtres] -j [action]
```

| Option        | Description                              |
|---------------|------------------------------------------|
| `-A`          | Ajoute une règle à une chaîne            |
| `-p`          | Protocole concerné (tcp, udp, icmp)       |
| `--dport`     | Port de destination                      |
| `-s` / `-d`   | IP source / destination                  |
| `-j`          | Action : `ACCEPT`, `DROP`, `REJECT`, etc |

---

## 📊 Chaînes principales

| Chaîne    | Rôle                                      |
|-----------|--------------------------------------------|
| `INPUT`   | Trafic entrant vers la machine              |
| `OUTPUT`  | Trafic sortant depuis la machine            |
| `FORWARD` | Trafic traversant la machine (routeur)      |

---

## 📁 Tables principales

| Table     | Usage                                      |
|-----------|--------------------------------------------|
| `filter`  | Filtrage des paquets (par défaut)           |
| `nat`     | Redirection/NAT des connexions              |
| `mangle`  | Modification de paquets (TTL, marquage...)  |

---

## 🔧 Exemples de règles commentées

### Autoriser loopback (localhost)
```bash
iptables -A INPUT -i lo -j ACCEPT
```

### Politique par défaut stricte
```bash
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT
```

### Autoriser ping (ICMP)
```bash
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
```

### Autoriser SSH (port 22)
```bash
iptables -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT
```

### Autoriser HTTP/HTTPS
```bash
iptables -A INPUT -p tcp -m multiport --dports 80,443 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp -m multiport --sports 80,443 -m state --state ESTABLISHED -j ACCEPT
```

### Autoriser une IP WAN à accéder à un port spécifique
```bash
iptables -A INPUT -p tcp -s 203.0.113.42 --dport 54321 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 54321 -d 203.0.113.42 -m state --state ESTABLISHED -j ACCEPT
```

### Bloquer les autres connexions sur ce port
```bash
iptables -A INPUT -p tcp --dport 54321 -j DROP
```

---

## 🛡️ Limiter les connexions (anti-brute-force)

### Limiter SSH à 3 tentatives par minute (module `recent`)
```bash
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 60 --hitcount 3 --name SSH -j DROP
```

### Blocage temporaire avec TTL
```bash
iptables -A INPUT -p tcp --dport 22 -m recent --set --name SSH
iptables -A INPUT -p tcp --dport 22 -m recent --update --seconds 60 --hitcount 5 --rttl --name SSH -j DROP
```

### Limite de 3 connexions par minute avec `hashlimit`
```bash
iptables -A INPUT -p tcp --dport 22 -m hashlimit --hashlimit 3/min --hashlimit-burst 3 \
--hashlimit-mode srcip --hashlimit-name ssh_limit -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```

---

## 💾 Sauvegarde et nettoyage

### Sauvegarder les règles (Debian/Ubuntu)
```bash
sudo apt install iptables-persistent
iptables-save > /etc/iptables/rules.v4
```

### Nettoyer les règles
```bash
iptables -F
iptables -X
iptables -t nat -F
```

---

## ✅ Bonnes pratiques

- Toujours tester dans une session SSH secondaire.
- Documenter chaque règle dans un script.
- Utiliser `iptables -L -v -n --line-numbers` pour vérifier les règles.
- Pour activer les logs :
  ```bash
  iptables -A INPUT -j LOG --log-prefix "iptables INPUT DROP: " --log-level 4
  ```

---

## 📜 Exemple de script iptables complet (pare-feu personnel de base)

```bash
#!/bin/bash

# Nettoyage des règles existantes
iptables -F
iptables -X
iptables -t nat -F

# Politique par défaut
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# Autoriser loopback
iptables -A INPUT -i lo -j ACCEPT

# Autoriser connexions établies
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Autoriser SSH (limité à 3 tentatives/min par IP)
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 60 --hitcount 3 --name SSH -j DROP
iptables -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT

# HTTP/HTTPS
iptables -A INPUT -p tcp -m multiport --dports 80,443 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp -m multiport --sports 80,443 -m state --state ESTABLISHED -j ACCEPT

# Exemple : accès restreint au port 54321 depuis IP WAN
iptables -A INPUT -p tcp -s 203.0.113.42 --dport 54321 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A INPUT -p tcp --dport 54321 -j DROP
iptables -A OUTPUT -p tcp --sport 54321 -d 203.0.113.42 -m state --state ESTABLISHED -j ACCEPT

# Logging optionnel
iptables -A INPUT -j LOG --log-prefix "[IPTABLES BLOCK] " --log-level 4
```

---

Ce script peut être rendu exécutable via `chmod +x firewall.sh`, puis lancé avec `sudo ./firewall.sh`.

---

---

<p align="center">
  🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessible à tous.
</p>
