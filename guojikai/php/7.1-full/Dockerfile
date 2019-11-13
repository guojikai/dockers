FROM php:7.1-fpm

ENV BUILD_DEPS \
    libssl-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libmemcached-dev \
    librdkafka-dev

COPY pecl_exts /usr/src/pecl_exts

RUN apt-get update && apt-get install -y $BUILD_DEPS\
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-install -j$(nproc) mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install -j$(nproc) opcache \
    && echo "Install PHP extensions via PECL local Packages" \
    && pecl install /usr/src/pecl_exts/mongodb-1.2.8.tgz \
    && pecl install /usr/src/pecl_exts/redis-3.1.2.tgz \
    && pecl install /usr/src/pecl_exts/memcached-3.0.3.tgz \
    && pecl install /usr/src/pecl_exts/rdkafka-3.0.1.tgz \
    && pecl install /usr/src/pecl_exts/swoole-1.9.12.tgz \
    # && echo "Install PHP extensions via PECL..." \
    # && pecl install mongodb \
    # && pecl install redis \
    # && pecl install memcached \
    # && pecl install rdkafka \
    # && pecl install swoole \
    && docker-php-ext-enable \
        mongodb redis memcached rdkafka swoole \
    && rm -rf /usr/src/pecl_exts \
    #composer
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update

