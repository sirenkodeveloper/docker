FROM php:8.0-apache

RUN apt-get update -y && apt-get install -y sendmail libpng-dev

RUN apt-get install -y libjpeg-dev

RUN apt-get install -y libfreetype6-dev

RUN apt-get -y install locales gettext

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/

RUN docker-php-ext-install gd

RUN docker-php-ext-install mysqli pdo pdo_mysql

RUN a2enmod rewrite

RUN docker-php-ext-enable gd

RUN docker-php-ext-install gettext

RUN docker-php-ext-enable gettext

ENV PHP_DATE_TIMEZONE="Europe/Kiev"
ENV PHP_MEMORY_LIMIT="384M"
ENV PHP_POST_MAX_SIZE="256M"
ENV PHP_UPLOAD_MAX_FILESIZE="192M"

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.start_with_request=yes" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_host = host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
