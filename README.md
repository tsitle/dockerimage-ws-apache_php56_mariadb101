# Docker Image

For hosting PHP powered websites.

## Inheritance
- Docker Image **ws-apache\_base**
	- PHP 5.6 (CLI + FPM)
	- PHP packages (see below)
	- MariaDB Client 10.1 (^= MySQL 5.7)
	- php-pear
	- xml-core

## PHP Packages included
- bcmath
- cli
- common
- curl
- fpm
- gd
- imagick
- imap
- json
- mbstring
- mcrypt
- mysql
- opcache
- readline
- sqlite3
- xdebug
- xml
- zip

## Webserver TCP Port
The webserver is listening only on TCP port 80 by default.

## Docker Container configuration
- CF\_DOCROOT [string]: Document Root directory (e.g. "/var/www/html")
- CF\_WEBROOT [string]: Website Root directory (e.g. "/var/www/html")
- CF\_WEBROOT\_SITE [string]: Subdirectory of CF\_WEBROOT to be used as actual Website Root directory (e.g. for Neos CMS "Web/")
- CF\_PROJ\_PRIMARY\_FQDN [string]: FQDN for website (e.g. "mywebsite.localhost")
- CF\_SET\_OWNER\_AND\_PERMS\_WEBROOT [bool]: Recursively chown and chmod CF\_WEBROOT?
- CF\_WWWDATA\_USER\_ID [int]: User-ID for www-data
- CF\_WWWDATA\_GROUP\_ID [int]: Group-ID for www-data
- CF\_WWWFPM\_USER\_ID [int]: User-ID for wwwphpfpm
- CF\_WWWFPM\_GROUP\_ID [int]: Group-ID for wwwphpfpm

## Enabling the PHP Module XDebug
The PHP Module 'xdebug' is disabled by default.  
To enable it you'll need to follow these steps from within a Bash shell:  
(replace "DOCKERCONTAINER" with your Docker Container's name)

1. Start the Docker Container
2. If your debugger (e.g. IntelliJ) is running on a different machine then
	you'll need to replace the default hostname "host" with your machine's hostname.  
	Edit XDebug configuration:  
	```
	$ docker exec -it DOCKERCONTAINER nano /etc/php/5.6/mods-available/xdebug.ini
	```  
	  
	```
	xdebug.remote_host="host"
	```  
	When done editing hit CTRL-X, then "J" and hit ENTER
3. Now enable the PHP Module:  
	```  
	$ docker exec -it DOCKERCONTAINER phpenmod xdebug
	```  
	```  
	$ docker exec -it DOCKERCONTAINER service php5.6-fpm restart
	```

## Disabling the PHP Module XDebug
```  
$ docker exec -it DOCKERCONTAINER phpdismod xdebug
```  
```  
$ docker exec -it DOCKERCONTAINER service php5.6-fpm restart
```
