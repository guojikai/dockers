FROM php:8.3-fpm-alpine3.20

# deps
ENV BUILD_DEPS="autoconf gcc g++ make zlib-dev openssl-dev libpng-dev freetype-dev jpeg-dev libzip-dev libpq-dev"

# update packages list & install dependences
RUN apk update && apk add ${BUILD_DEPS} 

# install exts
RUN echo "Install PHP extensions via docker-php-ext-install..." \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) opcache 

RUN echo "Install PHP extensions via PECL..." \
    && pecl update-channels \
    && pecl install redis \
    && docker-php-ext-enable redis 

# install composer
RUN echo "Install Composer..." \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update

# clean
RUN apk del ${BUILD_DEPS} && apk del ${BUILD_DEPS}