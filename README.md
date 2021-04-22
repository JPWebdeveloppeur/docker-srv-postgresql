# Docker environnement Php 7.4.16-apache for Symfony 4.4

Il s'agit d'une image Docker qui vous permet d'avoir un environnement de développement local ( Php 7.4.16, Apache 2.4.38, PostgreSql 11.11, Pgadmin4).

Outre l'image de base Apache PHP 7.4.16, il comprend également les modules suivants:
```
* apcu 			* intl 				* Phar
* calendar 		* json 				* posix
* Core 			* libxml 			* readline
* ctype 		* mbstring 			* Reflection
* curl 			* mysqlnd 			* session
* date 			* openssl 			* SimpleXML
* dom 			* pcre 				* sodium
* fileinfo 		* PDO 				* SPL
* filter 		* pdo_mysql 		        * sqlite3
* ftp 			* PDO_ODBC 			* standard
* gd 			* pdo_pgsql 		        * tokenizer
* hash 			* pdo_sqlite 		        * xml
* iconv 		* pgsql 			* xmlreader
* xmlwriter 	        * xsl 				* Zend OPcache
* zip 			* zlib
```

**Note:**  Vous pouvez s'il vous souhaitait rajouter des extensions via le [Dockerfile](docker/php/dockerfile)

### Comment ça marche ?

* Pendant que vous développez votre application, vous utilisez `docker-compose` qui utilise la base` Dockerfile` et monte votre dossier local `/project` à l'intérieur. 

* Cela signifie que vous pouvez développer votre application sans redémarrer le conteneur. 

* Le `docker-compose` démarre également une base de données psql et le conteneur pgadmin pour une administration facile.
  
* NodeJs, npm, yarn, vim sont emnbarqué au sein du conteneur php. 

# Démarrage de l'environnement de développement avec PHP, MySQL et phpMyAdmin 

➔ Ouvrez un terminale type bash et placez-vous dans le répertoire ou se trouve le docker-compose puis saisir :

```
docker-compose up -d ou docker-compose up --build
```
➔ Pour accéder à votre conteneur, il faut lancer la commande suivante :
```
  docker exec -it docker_php_apache usr/bin/zsh
```
➔ Lancer l'installation de symfony : 
```
   composer create-project symfony/website-skeleton:"^4.4" my_project_name
```

➔ Voici l'url pour l'applicationweb :

    ► Application Web : 
        * http://localhost:8741/

    ► Phpmyadmin :
        * http://localhost:8080/


### Identifiants MySQL

➔ Une base de données MySQL vide par défaut est configurée que vous pouvez utiliser dans votre application :

* User: `docker_db`
* Password: `docker_db`
* Database name: `docker_db_test`
* Database host: `db_docker`

# Structure des dossiers

```
- /docker # Repertoire parents
    - /docker/db # Permet de pouvoir au besoin stocker vos dump db
    - /docker/php # Contient le dockerfile
    - /docker/php/vhosts # Contient le vhost.conf pour la config apache
- /docker-compose.yml # Orchestrer vos conteneurs
```
# Composer

➔ Il y a un fichier Composer vide à la racine. Vous pouvez ajouter vos dépendances de projet ici.

# Memento Docker
➔ https://labo-tech.fr/base-de-connaissance/quelles-sont-les-commandes-de-base-de-docker/

➔ https://wiki.maxcorp.org/docker-les-commandes-utiles/