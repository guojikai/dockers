FROM php:7.0-fpm
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libmemcached-dev \
        librdkafka-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install -j$(nproc) opcache \
    && pecl install redis-3.1.2 \
    && pecl install memcached-3.0.0 \
    && pecl install rdkafka-2.0.1 \
    && pecl install swoole-1.9.12 \
    && docker-php-ext-enable redis memcached rdkafka swoole
