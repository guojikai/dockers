FROM php:8.3-fpm-bookworm

# deps
ENV BUILD_DEPS="libbz2-dev libfreetype6-dev libjpeg-dev libpng-dev libwebp-dev libxpm-dev libzip-dev"

# update packages list & install dependences
RUN apt-get update && apt-get install -y --no-install-recommends ${BUILD_DEPS} 

# install exts
RUN echo "Install PHP extensions via docker-php-ext-install..." \
    && docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp --with-xpm \
    && docker-php-ext-install -j$(nproc) bz2 \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-install -j$(nproc) opcache \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-install -j$(nproc) bcmath 

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
RUN apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && rm -rf /var/lib/apt/lists/*