# vim: set foldmarker=[[,]] foldlevel=0 foldmethod=marker spell:
# ------------------------------------------------------------------------------
# -> 1. Base image [[
# ------------------------------------------------------------------------------

FROM php:5.6-fpm-alpine

# ]]
# ------------------------------------------------------------------------------
# -> 2. Install base packages [[
# ------------------------------------------------------------------------------

RUN apk update && apk add --no-cache \
    git \
    wget \
    ssmtp \
    autoconf \
    build-base \
    libxml2-dev \
    libmcrypt-dev \
    openssl-dev

# ]]
# ------------------------------------------------------------------------------
# -> 3. Install PHP extensions [[
# ------------------------------------------------------------------------------

RUN docker-php-ext-install \
    curl \
    gd \
    mbstring \
    mysqli \
    mcrypt \
    mysql \
    pdo_mysql \
    soap \
    zip \
    xsl \
    opcache \
    bcmath

# Install & enable mongo
RUN pecl install mongodb \
    && docker-php-ext-enable mongodb

# ]]
# ------------------------------------------------------------------------------
# -> 4. Install Xdebug [[
# ------------------------------------------------------------------------------

ENV XDEBUG_VERSION 2.4.1
RUN wget http://xdebug.org/files/xdebug-$XDEBUG_VERSION.tgz \
    && tar -zxvf xdebug-$XDEBUG_VERSION.tgz && cd xdebug-$XDEBUG_VERSION \
    && phpize && ./configure --enable-xdebug && make && make install

# ]]
# ------------------------------------------------------------------------------
# -> 5. Composer [[
# ------------------------------------------------------------------------------

RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer
RUN php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer \
    && rm -rf /tmp/composer-setup.php

# ]]
# ------------------------------------------------------------------------------
# -> 6. Magerun [[
# ------------------------------------------------------------------------------

RUN curl -o magerun https://raw.githubusercontent.com/netz98/n98-magerun/master/n98-magerun.phar \
    && chmod +x ./magerun \
    && mv ./magerun /usr/local/bin/

# ]]
# ------------------------------------------------------------------------------
# -> 7. Configure [[
# ------------------------------------------------------------------------------

COPY config/php.ini /usr/local/etc/php/php.ini
COPY config/ssmtp.conf /etc/ssmtp/ssmtp.conf

# ]]
# ------------------------------------------------------------------------------
# -> 8. Users [[
# ------------------------------------------------------------------------------

# Add new user for uid 1000
RUN adduser -D -u 1000 devbox

# Change user
USER devbox

# ]]
# ------------------------------------------------------------------------------
