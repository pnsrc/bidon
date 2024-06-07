FROM php:8.1-fpm-alpine

RUN apk --no-cache add \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libwebp-dev \
    libxpm-dev \
    libzip-dev \
    tzdata \
    autoconf \
    g++ \
    make

RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp --with-xpm \
    && docker-php-ext-install gd mysqli pdo pdo_mysql zip \
    && pecl install redis \
    && docker-php-ext-enable redis

RUN chmod -R 777 /var/www/html/

COPY php.ini /usr/local/etc/php/php.ini
