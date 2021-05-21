# Mise à jour en ligne de commande de jeedom

Nous allons voir ici comment faire une mise à jour manuellement sur

## Prérequis

-   savoir se connecter en SSH à Jeedom
-   connaître les identifiants SSH (voir documentation d’installation)
-   avoir un accès Internet depuis la box Jeedom

> **Important**
>
> Pensez bien à faire et exporter une sauvegarde avant toute mise à jour manuelle.

## Téléchargement et décompression

En SSH, faites :

````
sudo su -
cd /root
wget https://github.com/jeedom/core/archive/master.zip
unzip master.zip
cp -R core-master/* /var/www/html
cp -R core-master/.[^.]* /var/www/html
````

## Mise à jour

Toujours en SSH:

````
sudo su -
php /var/www/html/install/update.php mode=force
chmod 775 -R /var/www/html
chown www-data:www-data -R /var/www/html
````

> **Important**
>
> Si votre installation de Jeedom est un peu ancienne, il faut remplacer tous les ``/var/www/html`` par ``/usr/share/nginx/www/jeedom``


## En cas de problème SQL

Si la mise à jour ne se fait pas et retourne un message d'erreur SQL (par exemple : "[MySQL] Error code : 42S22 (1054)"), essayez ceci (toujours en SSH):
````
sudo su -
php /var/www/html/install/database.php
````

> **Important**
>
> Pensez à relancer les étapes du chapitre **Mise à jour** si ce script ne retourne pas d'erreur.
