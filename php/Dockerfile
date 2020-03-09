FROM php:7.3-fpm-alpine
MAINTAINER drupal-docker

RUN apk add --no-cache --virtual .dd-build-deps libpng-dev libjpeg-turbo-dev postgresql-dev libxml2-dev libzip-dev gnu-libiconv $PHPIZE_DEPS \
   && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
   && docker-php-ext-install gd mbstring pdo_mysql pdo_pgsql zip \
   && docker-php-ext-install opcache bcmath soap \
   && pecl install redis-3.1.1 \
   && pecl install xdebug \
   && docker-php-ext-enable redis \
   && docker-php-ext-enable xdebug \
   && apk add --no-cache libpng libjpeg libpq libxml2 mariadb-client gnu-libiconv \
   && apk del .dd-build-deps

# This needs in order to run xdebug from PhpStorm
ENV PHP_IDE_CONFIG 'serverName=DockerApp'
ENV LD_PRELOAD="/usr/lib/preloadable_libiconv.so php-fpm php"

COPY drupal-*.ini /usr/local/etc/php/conf.d/
# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
