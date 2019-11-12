FROM php:7.2-fpm-stretch

ENV BUILD_DEPS \
    zlib1g-dev \
    libssl-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libmemcached-dev \
    librdkafka-dev

ENV DEV_SOFTS \
    inetutils-ping \
    procps \
    wget \
    vim

COPY sources.list /usr/src/sources.list.mirror
COPY pecl_exts /usr/src/pecl_exts

RUN echo "Build start..." \
    && echo "Change sources to USTC Mirror..." \
    && mv /etc/apt/sources.list /usr/src/sources.list.backup \
    && cp /usr/src/sources.list.mirror /etc/apt/sources.list \
    && apt-get update \
    && echo "Intall dependencies..." \
    && apt-get install -y $BUILD_DEPS \
    && echo "Intall dev softs..." \
    && apt-get install -y $DEV_SOFTS \
    && echo "Intall PHP extensions..." \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install -j$(nproc) opcache \
    && echo "Intall PHP extensions via PECL and local Packages..." \
    && pecl install /usr/src/pecl_exts/mcrypt-1.0.1.tgz \
    && pecl install /usr/src/pecl_exts/mongodb-1.3.4.tgz \
    && pecl install /usr/src/pecl_exts/redis-3.1.2.tgz \
    && pecl install /usr/src/pecl_exts/memcached-3.0.3.tgz \
    && pecl install /usr/src/pecl_exts/rdkafka-3.0.1.tgz \
    && pecl install /usr/src/pecl_exts/swoole-1.9.12.tgz \
    && docker-php-ext-enable mcrypt mongodb redis memcached rdkafka swoole \
    && rm -rf /usr/src/pecl_exts \
    && echo "Intall PHP Composer..." \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update