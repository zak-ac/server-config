## Introduction
Iptables est un utilitaire en ligne de commande qui permet de gérer les règles de pare-feu au niveau du noyau Linux. Il est puissant et flexible, offrant de nombreuses options pour filtrer et modifier le trafic réseau.

Ce guide suppose une connaissance de base du fonctionnement du réseau et des commandes Linux. Il fournit des instructions pas à pas pour démarrer avec iptables.

## Prérequis
Avant de commencer, assurez-vous d'avoir les éléments suivants :

Un système Linux avec iptables installé.
Accès en tant que superutilisateur (root) ou utilisateur disposant de droits sudo.
## Installation
Si vous n'avez pas encore iptables installé sur votre système, vous pouvez l'installer en utilisant le gestionnaire de paquets de votre distribution. Par exemple, pour Ubuntu ou Debian :

```
sudo apt-get update
sudo apt-get install iptables
```

## Configuration de base

```
#!/bin/sh

# Réinitialiser toutes les règles existantes
iptables -t filter -F
iptables -t filter -X

# Politique par défaut pour les chaînes INPUT, FORWARD et OUTPUT
iptables -t filter -P INPUT DROP
iptables -t filter -P FORWARD DROP
iptables -t filter -P OUTPUT DROP

# Autoriser les connexions établies ou connexions associées
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -m state --state RELATED,ESTABLISHED -j ACCEPT

# Autoriser les requêtes ICMP (ping)
iptables -t filter -A INPUT -p icmp -j ACCEPT
iptables -t filter -A OUTPUT -p icmp -j ACCEPT

# Autoriser les connexions locales (loopback)
iptables -t filter -A INPUT -i lo -j ACCEPT
iptables -t filter -A OUTPUT -o lo -j ACCEPT

# Autoriser les connexions entrantes sur le port TCP 1234
iptables -t filter -A INPUT -p tcp --dport 1234 -j ACCEPT
iptables -t filter -A OUTPUT -p tcp --dport 1234 -j ACCEPT

# Autoriser les connexions sur les ports TCP et UDP 53 (DNS)
iptables -t filter -A INPUT -p tcp --dport 53 -j ACCEPT
iptables -t filter -A OUTPUT -p tcp --dport 53 -j ACCEPT
iptables -t filter -A INPUT -p udp --dport 53 -j ACCEPT
iptables -t filter -A OUTPUT -p udp --dport 53 -j ACCEPT

# Autoriser les connexions sortantes sur le port UDP 123
iptables -t filter -A OUTPUT -p udp --dport 123 -j ACCEPT

# Autoriser les connexions sortantes sur les ports TCP 80 (HTTP) et 443 (HTTPS)
iptables -t filter -A OUTPUT -p tcp --dport 80 -j ACCEPT
iptables -t filter -A OUTPUT -p tcp --dport 443 -j ACCEPT

# Autoriser les connexions entrantes sur les ports TCP 80 (HTTP), 443 (HTTPS) et 8443
iptables -t filter -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -t filter -A INPUT -p tcp --dport 443 -j ACCEPT
iptables -t filter -A INPUT -p tcp --dport 8443 -j ACCEPT

# Autoriser les connexions sortantes sur les ports TCP 20 et 21 pour FTP
# Note : décommenter la ligne suivante si vous utilisez le module ip_conntrack_ftp
# modprobe ip_conntrack_ftp
iptables -t filter -A OUTPUT -p tcp --dport 20:21 -j ACCEPT

# Autoriser les connexions entrantes sur les ports TCP 20 et 21 pour FTP
iptables -t filter -A INPUT -p tcp --dport 20:21 -j ACCEPT
```
## Sauvegarde et restauration des règles
