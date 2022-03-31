FROM php:8.1-fpm-buster

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:2.2 /usr/bin/composer /usr/bin/composer

# Node.js と NPM
#RUN apt-get -y update
#RUN apt-get install -y \
#    curl \
#    gnupg
#RUN curl -sl https://rpm.nodesource.com/setup_16.x | bash -
#RUN apt-get install -y nodejs
#RUN npm install npm@latest -g

# install Node.js
COPY --from=node:16.14 /usr/local/bin /usr/local/bin
COPY --from=node:16.14 /usr/local/lib /usr/local/lib

RUN apt-get update && \
  apt-get -y install --no-install-recommends git unzip libzip-dev libicu-dev libonig-dev && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  docker-php-ext-install intl pdo_mysql zip bcmath

COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /data