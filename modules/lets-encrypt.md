# Configurer Let's Encrypt avec Nginx

Ce guide vous explique comment configurer un certificat SSL/TLS gratuit à l'aide de Let's Encrypt avec Nginx. Le certificat SSL/TLS permet de sécuriser votre site web et de chiffrer les communications entre les utilisateurs et le serveur.

## Prérequis

Avant de commencer, assurez-vous de disposer des éléments suivants :

- Un serveur Debian installé et fonctionnel.
- Nginx installé sur votre serveur Debian.

## Étapes de configuration

Suivez les étapes ci-dessous pour configurer Let's Encrypt avec Nginx :

1. **Installation de Certbot**

   - Utilisez la commande suivante pour installer Certbot :

     ```bash
     sudo apt-get update
     sudo apt-get install certbot
     ```

2. **Générer le certificat SSL/TLS avec Let's Encrypt**

   - Exécutez la commande suivante pour obtenir et installer automatiquement un certificat :

     ```bash
     sudo certbot --nginx
     ```

   - Suivez les instructions à l'écran pour fournir votre adresse e-mail et accepter les termes et conditions.

3. **Configuration de Nginx pour utiliser le certificat**

   - Ouvrez le fichier de configuration de votre site Nginx :

     ```bash
     sudo nano /etc/nginx/sites-available/votre_site
     ```

   - Ajoutez les lignes suivantes dans la section du serveur virtuel :

     ```nginx
     listen 443 ssl;
     ssl_certificate /etc/letsencrypt/live/votre_site/fullchain.pem;
     ssl_certificate_key /etc/letsencrypt/live/votre_site/privkey.pem;
     ```

   - Sauvegardez et fermez le fichier de configuration.

4. **Redémarrage du service Nginx**

   - Redémarrez le service Nginx pour appliquer les modifications :

     ```bash
     sudo service nginx restart
     #sudo /snap/bin/certbot --nginx
     ```

5. **Renouvellement automatique du certificat**

   - Certbot configure automatiquement le renouvellement du certificat avant son expiration. Aucune intervention manuelle n'est nécessaire.

## Informations supplémentaires

- Pour vérifier la validité du certificat, vous pouvez utiliser des outils en ligne ou des extensions de navigateur telles que SSL Labs Server Test ou Let's Encrypt Certificate Expiry Checker.
- Pour en savoir plus sur l'utilisation de Let's Encrypt avec Nginx, consultez la documentation officielle de Let's Encrypt (https://letsencrypt.org/docs/).
- N'oubliez pas de surveiller les notifications de renouvellement de certificat pour vous assurer que votre site reste sécurisé.
