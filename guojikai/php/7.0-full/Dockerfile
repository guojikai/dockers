FROM php:7.0-fpm

ENV BUILD_DEPS \
    libssl-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libmemcached-dev \
    librdkafka-dev

RUN apt-get update && apt-get install -y $BUILD_DEPS\
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) pdo \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install -j$(nproc) opcache \
    && echo "Intall PHP extensions via PECL..." \
    && pecl install mongodb \
    && pecl install redis \
    && pecl install memcached \
    && pecl install rdkafka \
    && pecl install swoole \
    && docker-php-ext-enable \
        mongodb redis memcached rdkafka swoole \
    #composer
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update

