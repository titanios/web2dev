FROM php:fpm-alpine

# ADD ./php-fpm-additional.conf /usr/local/etc/php/conf.d

ENV PHP_OPCACHE_VALIDATE_TIMESTAMPS="0" \
    PHP_OPCACHE_MAX_ACCELERATED_FILES="10000" \
    PHP_OPCACHE_MEMORY_CONSUMPTION="192" \
    PHP_OPCACHE_MAX_WASTED_PERCENTAGE="10"

RUN apk update && apk upgrade && apk add icu-dev \
    && docker-php-ext-install mysqli pdo pdo_mysql \
    && docker-php-ext-install opcache \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl