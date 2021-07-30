![Repo Image](https://github.com/lalantham/web-server-linux/blob/master/img.png)
# LAMP on Arch

>Complete Guild for install apache, php, mysql in linux and configure 

## 01 - Apache

	1.1 	Install Apache Server
				sudo pacman -S apache

	1.2 - Comment this Line
			#LoadModule unique_id_module modules/mod_unique_id.so

## 02 - PHP

	2.1 - Install PHP
			sudo pacman -S php php-apache
	2.2 - PHP Configs
	      sudo nano /etc/php/php.ini
	      		date.timezone = Asia/Colombo

## 03 - PHP Mysql Module

	2.1 - /etc/httpd/conf/httpd.conf
		#LoadModule mpm_event_module modules/mod_mpm_event.so
       		LoadModule mpm_prefork_module modules/mod_mpm_prefork.so
      	    - Place this at the end of the LoadModule list:
       	        LoadModule php_module modules/libphp.so
	        AddHandler php-script .php
            - Place this at the end of the Include list:
                Include conf/extra/php_module.conf
            - sudo nano  /etc/php/php.ini
	        extension=mysqli

## 04 - Mysql

	4.1 - Install mysql
      	      sudo pacman -S mysql
      
      	     sudo su
             cd /var/lib/mysql
             rm -r *
      
             mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
             systemctl start mysqld
             systemctl start mysql.service
             systemctl start mariadb
             mysql (Check)
             sudo mysql_secure_installation
      
         MySql Password
             mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
             mysql -u root
             MariaDB [(none)]> use mysql
             MariaDB [mysql]> flush privileges;
             MariaDB [mysql]> ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
             MariaDB [mysql]> exit     
	     
## 05 - PHPMyAdmin

	4.1 - Install phpmyadmin
      	      sudo pacman -S phpmyadmin
      
      	      sudo gedit /etc/php/php.ini
              Uncomment = extension=mysqli, extension=pdo_mysql
        5.2 phpmyadmin configs
	      sudo touch /etc/httpd/conf/extra/phpmyadmin.conf
	      sudo nano /etc/httpd/conf/extra/phpmyadmin.conf
	      		Alias /phpmyadmin "/usr/share/webapps/phpMyAdmin"
			<Directory "/usr/share/webapps/phpMyAdmin">
			    DirectoryIndex index.php
			    AllowOverride All
			    Options FollowSymlinks
			    Require all granted
			</Directory>
	5.3 httpd config
	     sudo gedit /etc/httpd/conf/httpd.conf
		# phpMyAdmin configuration
		Include conf/extra/phpmyadmin.conf
      
## 06 - Extras

	4.1 - Virual Host Custom Script
			https://github.com/lalantham/virtualhost
