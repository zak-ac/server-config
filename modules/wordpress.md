# Installation de WordPress sur un serveur Debian

Ce document fournit une documentation détaillée sur l'installation et la configuration de WordPress sur un serveur Debian. Suivez les étapes ci-dessous pour mettre en place votre site WordPress.

## Prérequis

- Debian
- Nginx
- MariaDB /MySQL
- PHP

**Note :** Ce tutoriel utilise `example.com` comme nom de domaine pour l'illustration. Assurez-vous d'avoir un nom de domaine et de configurer l'enregistrement DNS A pour pointer vers l'adresse IP de votre serveur.

## Étapes d'installation

1. **Mise à jour du système**

   Connectez-vous à votre serveur via SSH et mettez à jour le système en exécutant la commande suivante :

  ```bash
   sudo apt update && sudo apt upgrade
  ```

2. **Installation du serveur web Nginx**

Utilisez la commande apt pour installer Nginx :

  ```bash
   sudo apt install nginx
   ```
3. **Installation et sécurisation de la base de données**

Installez MariaDB, une version populaire de MySQL :

   ```bash
   sudo apt install mariadb-server php-mysql
   ```
Ensuite, sécurisez l'installation de la base de données en exécutant la commande suivante et en répondant "Y" aux options de configuration de sécurité :

   ```bash
   sudo mysql_secure_installation
   ```
4. **Installation de PHP**

Installez PHP FPM (FastCGI Process Manager) pour interpréter les requêtes PHP :

   ```bash
   sudo mysql_secure_installation
   ```
Pour des raisons de sécurité, ouvrez le fichier `/etc/php/7.2/fpm/php.ini` avec un éditeur de texte et modifiez la ligne `fix_pathinfo` comme suit :

   ```bash
   fix_pathinfo=0
   ```
5. **Installation de WordPress**

Téléchargez et installez la dernière version de WordPress depuis le site officiel :

   ```bash
   cd /var/www
   mkdir example.com
   cd example.com
   wget https://wordpress.org/latest.tar.gz
   tar -xzvf latest.tar.gz
   rm latest.tar.gz
   cd wordpress
   ```

6. **Configuration de la base de données pour WordPress**

Créez une base de données pour WordPress et un utilisateur avec les privilèges appropriés. Accédez à la ligne de commande MySQL en tapant `mysql` :

 ```sql
 create database example_db default character set utf8 collate utf8_unicode_ci;
 create user 'example_user'@'localhost' identified by 'example_pw';
 grant all privileges on example_db.* TO 'example_user'@'localhost';
 flush privileges;
 ```

7. **Connexion de WordPress à la base de données**

Faites une copie du fichier de configuration WordPress en utilisant la commande suivante :

```bash
 cp wp-config-sample.php wp-config.php
 ```
Ouvrez le fichier `wp-config.php` avec un éditeur de texte et modifiez les lignes suivantes en fonction des valeurs que vous avez fournies pour la base de données :

 ```bash
  define( 'DB_NAME', 'example_db' );
  define( 'DB_USER', 'example_user' );
  define( 'DB_PASSWORD', 'example_pw' );
 ```

Enfin, copiez les valeurs à partir de [ce lien](https://api.wordpress.org/secret-key/1.1/salt) et remplacez les valeurs dans le fichier `wp-config.php` sous la section "Authentication Unique Keys and Salts".

8. **Configuration de Nginx pour servir votre site WordPress**

La plupart des fichiers de configuration pour Nginx se trouvent dans `/etc/nginx`. Commencez par supprimer le fichier de configuration par défaut de Nginx :

 ```bash
 cd /etc/nginx
 rm sites-enabled/default
 ```
Ensuite, créez un fichier de configuration pour votre site WordPress dans `sites-available/example.conf` avec le contenu suivant ajusté en fonction de votre site :

 ```bash
  upstream example-php-handler {
     server unix:/var/run/php/php7.2-fpm.sock;
  }
  server {
   listen 80;
   server_name example.com www.example.com;
   root /var/www/example.com/wordpress;
   index index.php;
 location / {
   try_files $uri $uri/ /index.php?$args;
  }
 location ~ .php$ {
   include snippets/fastcgi-php.conf;
   fastcgi_pass example-php-handler;
  }
 }
```
Publiez votre site en créant un lien symbolique depuis le fichier `sites-available/example.conf` vers le répertoire `sites-enabled` :
   
 ```bash
   sudo ln -s /etc/nginx/sites-available/example.conf /etc/nginx/sites-enabled/
 ```
Enfin, testez les modifications de configuration de Nginx et redémarrez le serveur web :

 ```bash
   nginx -t
   systemctl restart nginx
 ```

9. **Configuration de WordPress**

Accédez à votre URL ou nom de domaine (dans cet exemple `example.com`) et vous verrez le processus d'installation de WordPress en cinq minutes. En réalité, il suffit d'environ une minute pour remplir ce formulaire.

Donnez un titre à votre site, choisissez un nom d'utilisateur et un mot de passe sécurisé.


