FROM php:7-fpm-alpine
ENV GUOJIKAI_PHP_DEPS \
        g++ \
        gcc \
        make \
        autoconf \
        libmcrypt libmcrypt-dev  \
        freetype freetype-dev  \
        libjpeg-turbo libjpeg-turbo-dev  \
        libpng libpng-dev \
        libmemcached librdkafka=0.9.5-r0
RUN apk add --no-cache $GUOJIKAI_PHP_DEPS \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && docker-php-ext-install -j${NPROC} iconv mcrypt \
    && docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j${NPROC} gd \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install -j${NPROC} opcache \
    && pecl install redis-3.1.2 \
    && pecl install memcached-3.0.0 \
    && pecl install rdkafka-2.0.1 \
    && pecl install swoole-1.9.12 \
    && docker-php-ext-enable redis memcached rdkafka swoole \
    && apk del --no-cache libmcrypt-dev freetype-dev libpng-dev libjpeg-turbo-dev \
    #composer
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update

