# Docker Image
# Apache 2.4 + PHP 5.6 (CLI + FPM) + MariaDB Client 10.1 (^= MySQL 5.7)

## Document Root
The website's sourcecode is located in '/var/www/html/'.

## Webserver TCP Port
The webserver is listening only on TCP port 80 by default.

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
