FROM surnet/alpine-wkhtmltopdf:3.19.0-0.12.6-small as wkhtmltopdf
FROM php:fpm-alpine

# ADD ./php-fpm-additional.conf /usr/local/etc/php/conf.d

# For dev env only useful, if you use a file watcher for recaching.
ENV PHP_OPCACHE_ENABLE="0" \
    PHP_OPCACHE_ENABLE_CLI="1" \
    PHP_OPCACHE_VALIDATE_TIMESTAMPS="0" \
    PHP_OPCACHE_MAX_ACCELERATED_FILES="10000" \
    PHP_OPCACHE_MEMORY_CONSUMPTION="192" \
    PHP_OPCACHE_MAX_WASTED_PERCENTAGE="10"

RUN apk update && apk upgrade && apk add --no-cache git icu-dev libzip-dev pcre-dev build-base autoconf php-pear zip \
    && pear config-set php_ini /usr/local/etc/php/conf.d/docker-fpm.ini \
#    && pecl install oauth \
    && apk add --no-cache libxrender libxext libxml2-dev libx11 libssl3 \
    && apk add --no-cache fontconfig freetype ttf-dejavu ttf-droid ttf-freefont ttf-liberation \
    && docker-php-ext-install mysqli pdo pdo_mysql \
    && docker-php-ext-install opcache \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-install xml dom zip

# Copy wkhtmltopdf files from docker-wkhtmltopdf
COPY --from=wkhtmltopdf /bin/wkhtmltopdf /bin/wkhtmltopdf
COPY --from=wkhtmltopdf /bin/libwkhtmltox* /bin/

# If necessary you can install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Clean up when done
RUN rm -rf /tmp/*