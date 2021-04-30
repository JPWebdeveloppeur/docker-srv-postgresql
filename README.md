# Docker environnement Php 7.4.16-apache for Symfony 4.4

Il s'agit d'une image Docker qui vous permet d'avoir un environnement de développement local ( Php 7.4.16, Apache 2.4.38, PostgreSql 11.11, Pgadmin 4).

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

* Pendant que vous développez votre application, vous utilisez `docker-compose` qui utilise la base `Dockerfile` et monte votre dossier local `/project` à l'intérieur se trouve votre application. 

* Cela signifie que vous pouvez développer votre application sans redémarrer le conteneur. 

* Le `docker-compose` démarre également une base de données postegre et le conteneur pgadmin pour une administration facile.
  
* Composer, NodeJs, npm, yarn, vim et zsh sont embarqué au sein du conteneur php. 

# Démarrage de l'environnement de développement avec PHP, PostgreSql et Pgadmin

➔ Ouvrez un terminal type bash et placez-vous dans le répertoire ou se trouve le docker-compose puis saisir :

```
docker-compose up -d ou docker-compose up --build
```
➔ Pour accéder à votre conteneur, il faut lancer la commande suivante :
```
  docker exec -it docker_php_apache usr/bin/zsh
```
➔ Lancer l'installation de symfony : 
```
   composer create-project symfony/website-skeleton:"^4.4" project
```

➔ Voici l'url pour l'application :

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
- /docker-compose.yml # Orchestrer vos conteneurs
- /project # contiendra votre application symfony 
```

# Memento Docker
➔ https://labo-tech.fr/base-de-connaissance/quelles-sont-les-commandes-de-base-de-docker/

➔ https://wiki.maxcorp.org/docker-les-commandes-utiles/
