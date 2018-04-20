# vim: set foldmarker=[[,]] foldlevel=0 foldmethod=marker spell:
# ------------------------------------------------------------------------------
# -> Base image [[
# ------------------------------------------------------------------------------

FROM php:fpm-alpine

# ]]
# ------------------------------------------------------------------------------
# -> Install base packages [[
# ------------------------------------------------------------------------------

RUN apk update && apk add \
    libxslt-dev \
    icu-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    g++ \
    make \
    autoconf \
    sqlite \
    git \
    wget \
    curl

# ]]
# ------------------------------------------------------------------------------
# -> Install PHP extensions [[
# ------------------------------------------------------------------------------

# Prepare gd extension
RUN docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/

RUN docker-php-ext-install \
    mbstring \
    tokenizer \
    bcmath \
    pdo_mysql \
    exif \
    xsl \
    intl \
    gd \
    soap \
    zip

# ]]
# ------------------------------------------------------------------------------
# -> Composer [[
# ------------------------------------------------------------------------------

RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
    && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer \
    && rm -rf /tmp/composer-setup.php

# ]]
# ------------------------------------------------------------------------------
# -> Install Xdebug [[
# ------------------------------------------------------------------------------

ARG XDEBUG_VERSION=2.6.0
RUN curl -LOk http://xdebug.org/files/xdebug-$XDEBUG_VERSION.tgz \
    && tar -zxvf xdebug-$XDEBUG_VERSION.tgz && cd xdebug-$XDEBUG_VERSION \
    && phpize && ./configure --enable-xdebug && make && make install

# ]]
# ------------------------------------------------------------------------------
# -> PHPunit [[
# ------------------------------------------------------------------------------

ARG PHPUNIT_VERSION=6.0
RUN curl -L -o phpunit https://phar.phpunit.de/phpunit-$PHPUNIT_VERSION.phar \
    && chmod +x ./phpunit \
    && mv ./phpunit /usr/local/bin/

# ]]
# ------------------------------------------------------------------------------
# -> Configure [[
# ------------------------------------------------------------------------------

# Set up config files
COPY config/php.ini /usr/local/etc/php/php.ini

# Change working directory
WORKDIR /var/www/project

# ]]
# ------------------------------------------------------------------------------
# -> Users [[
# ------------------------------------------------------------------------------

# Add & change user uid
RUN addgroup -g 1000 -S devbox
RUN adduser -u 1000 -S devbox -G devbox

USER devbox

# ]]
# ------------------------------------------------------------------------------
