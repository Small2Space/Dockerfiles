FROM php:8.1-apache
MAINTAINER smallru8
# ghcr.io/small2space/laravel:10
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN apt-get update -y && apt-get install -y openssl zip unzip git libonig-dev nodejs npm python3 python3-pip
#update node and npm
RUN npm cache clean -f
RUN npm install -g n
RUN n stable

RUN pip install passlib
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN docker-php-ext-install pdo mbstring pdo_mysql
RUN a2enmod rewrite
RUN composer global require "laravel/installer"
RUN composer global require "ecpay/sdk"
RUN composer global require "laravel/jetstream"
RUN composer global require "laravel/ui"
RUN composer global require "sudiptpa/guid"
#RUN composer global require "encore/laravel-admin"
WORKDIR /var/www/html
