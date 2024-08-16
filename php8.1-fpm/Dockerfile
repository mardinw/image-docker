FROM php:8.1-fpm-alpine

MAINTAINER Mardin Wijaya - https://github.com/mardinw

RUN apk update && apk add --no-cache freetype-dev \
    zip unzip libzip-dev \
    libjpeg-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    postgresql-dev \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd pdo zip mysqli pdo_mysql \
    && docker-php-ext-enable opcache
