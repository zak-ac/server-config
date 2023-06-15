# TLS

## TLS - Qu'est-ce que c'est ?
TLS (Transport Layer Security) est un protocole cryptographique utilisé pour sécuriser les communications sur un réseau. Il permet d'établir des connexions sécurisées et chiffrées entre un client et un serveur, assurant ainsi la confidentialité et l'intégrité des données échangées.

## TLS et HTTP
TLS joue un rôle crucial dans la sécurisation des connexions HTTP (Hypertext Transfer Protocol), communément appelées HTTPS. HTTPS est la version sécurisée de HTTP, où la communication entre le navigateur web du client et le serveur est chiffrée à l'aide de TLS. Ce chiffrement empêche l'accès non autorisé et protège les données contre l'interception ou la falsification.

## SSL vs TLS
SSL (Secure Sockets Layer) et TLS (Transport Layer Security) sont tous deux des protocoles cryptographiques utilisés pour des communications sécurisées. Cependant, TLS a largement remplacé SSL en tant que protocole préféré en raison de différentes vulnérabilités découvertes dans SSL.

Les versions de TLS ont évolué au fil du temps, avec TLS 1.0, TLS 1.1, TLS 1.2 et TLS 1.3 étant les principales versions. Chaque version apporte des améliorations en termes de sécurité, de performance et de compatibilité.

Il est important de noter que lorsqu'on parle de connexions sécurisées, le terme "SSL" est souvent utilisé de manière informelle, mais il implique généralement l'utilisation de TLS.

## Solutions pour la configuration de TLS

| Solution             | Let's Encrypt | EasyRSA               | Certtool              |
|----------------------|---------------|-----------------------|-----------------------|
| Coût                 | Gratuit       | Gratuit               | Gratuit               |
| Reconnaissance       | Reconnu par les navigateurs | Certificats auto-signés ou nécessitant une installation manuelle | Certificats auto-signés ou nécessitant une installation manuelle |
| Automatisation       | Processus de renouvellement automatisé | Processus de gestion manuel | Processus de gestion manuel |
| Autorité de certification (CA) | Utilise l'autorité de certification Let's Encrypt | Vous pouvez créer votre propre CA | Vous pouvez créer votre propre CA |
| Configuration avancée | Configuration basée sur Certbot | Permet une configuration et personnalisation avancées | Permet une configuration et personnalisation avancées |
| Environnements       | Convient à la plupart des environnements, y compris les sites web publics | Convient aux environnements privés ou internes | Convient aux environnements privés ou internes |

=========================

## Configuration de TLS

* [Configuration de TLS avec Let's Encrypt et Nginx](modules/lets-encrypt.md)
* [Configuration de TLS avec EasyRSA](modules/lets-encrypt.md)
* [Configuration de TLS avec Certtool](modules/lets-encrypt.md)
