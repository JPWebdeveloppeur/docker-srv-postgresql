# Docker environnement Php 7.4.25-apache for Symfony 4.4

Il s'agit d'une image Docker qui vous permet d'avoir un environnement de développement local ( Php 7.4.25, Apache 2.4.38, PostgreSql 11.11, Pgadmin 4).

Outre l'image de base Apache PHP 7.4.25, il comprend également les modules suivants:
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

**Note:**  Vous pouvez, si vous le souhaitez, ajouter des extensions via le [Dockerfile](docker/php/dockerfile)

### Comment ça marche ?

* Pendant que vous développez votre application, vous utilisez `docker-compose` qui utilise la base `Dockerfile` et monte votre application à la racine. 

* Le [docker-compose](docker-compose.yml) démarre également une base de données postegre et le conteneur pgadmin pour une administration facile.
  
* Composer, NodeJs, npm, yarn, vim et zsh sont embarqué au sein du conteneur php. 

# Démarrage de l'environnement de développement avec PHP, PostgreSql et Pgadmin

➔ Ouvrez un terminal type bash et placez-vous dans le répertoire ou se trouve le docker-compose puis saisir :

```
docker-compose up -d ou docker-compose up --build
```
➔ Pour accéder à votre conteneur apache /php , il faut lancer la commande suivante :
```
  docker exec -it docker_php_apache usr/bin/zsh
```
➔ Pour accéder à votre conteneur postgre , il faut lancer la commande suivante :
```
  docker exec -it db_docker psql --host=localhost --username=username --dbname=dbname
```
➔ Lancer l'installation de symfony : 
```
   composer create-project symfony/website-skeleton:"^4.4" project
```
➔ Si votre projet existe, suivre cette procédure [Procédure](README-procédure.md) pour la remise en route de votre application

➔ Url :

    ► Application Web : 
        * http://localhost:8741/

    ► Phpmyadmin :
        * http://localhost:8080/


### Identifiants PostgreSql

➔ Une base de données PostgreSql vide par défaut est configurée que vous pouvez utiliser dans votre application :

* POSTGRES_USER: `docker_db`
* POSTGRES_PASSWORD: `docker_db`
* POSTGRES_DB: `docker_db_test`
* POSTGRES_Hote: `localhost`

➔ Connexion bdd
```
psql --host=localhost --username=username --dbname=dbname
```
➔ Restore bdd
```
psql -U user name_db < chemin ou se trouve le backup
```

# Structure des dossiers

```
- /docker # Repertoire parents
    - /docker/db # Permet de pouvoir au besoin stocker vos dump db
    - /docker/php # Contient le dockerfile
    - /docker/php/vhosts # Contient le vhost.conf pour la config apache
- docker-compose.yml # Orchestrer vos conteneurs 
```

# Memento Docker 
➔ https://labo-tech.fr/base-de-connaissance/quelles-sont-les-commandes-de-base-de-docker/

➔ https://wiki.maxcorp.org/docker-les-commandes-utiles/

