Apache / PHP container for Joybird ( Automated Build ) 
=====================================

# PHP ini files


Adding PHP ini config files to container
--------

The container's PHP is configured with --with-config-file-scan-dir, so PHP will load all files in /etc/php.d/*.ini as configuration files. Pull this repo, place and commit your php.ini files and push.

````
j-apache
 |---/Dockerfile
 |---/php/conf.d   <-- Put any php config files here
 |---/README.md

````

Config files placed in php/conf.d directory in this repository will overwrite the settings in php.ini.


#### Example 999-php.ini
````
memory_limit = -1
error_reporting = E_ALL | E_STRICT
````


Putting config stuff here allows you to have custom settings while keeping updates simpler: if you modify php.ini itself then you either have to retain the old php.ini or overwrite it when you update PHP. If you keep your custom settings in, eg. conf.d/local.ini then you can update PHP easily while retaining any environment-specific settings.

The files are loaded in numeric order, so 000-php.ini is loaded before 001-php.ini.

Committing files to the repositry will generate a new build on docker hub automatically.


# About 

Features
--------

* Ability to set Apache document root through `APACHE_DOC_ROOT` environment variable. Default document root is `/var/www/html`
* Enabled Apache modules: rewrite
* Ability to set PHP `date.timezone` through `PHP_TIMEZONE` environment variable. Default timezone is `Europe/Rome`
* Enabled PHP extensions: gd, mcrypt, intl, mysql, mysqli, pdo_mysql, mbstring, soap, opcache, zip, xls
* Composer installed globally at `/usr/local/bin/composer`
* Xdebug PHP extension installed but not enabled
* Ability to enable xdebug PHP extension through `XDEBUG_ENABLE` environment variable which has to be set to `1`
* Ability to set xdebug.remote_enable setting through `HOST_IP` environment variable.
* GIT installed (required by Composer)
* sSMTP installed (as Mail Transfer Agent for PHP mail function)
* Ability to set sSMTP mailhub, AuthUser and AuthPass through `SSMTP_MAILHUB`, `SSMTP_AUTH_USER` and `SSMTP_AUTH_PASS` environment variables
* MySQL CLI Client installed

Usage
-----

Standalone usage example with host's current working directory as document root:

	$ docker run -p 80:80 -v $(pwd):/var/www/html webgriffe/php-apache-base

Building
-----
You can build the image locally from the directory containing the Dockerfile

	docker build -t joybird-apache




Props to webgriffe
