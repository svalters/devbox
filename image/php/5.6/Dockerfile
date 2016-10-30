# vim: set foldmarker=, foldlevel=0 foldmethod=marker spell:
# ------------------------------------------------------------------------------
# -> 1. Base image [[
# ------------------------------------------------------------------------------

FROM php:5.6-fpm

# ]]
# ------------------------------------------------------------------------------
# -> 2. Install base packages [[
# ------------------------------------------------------------------------------

RUN apt-get update && apt-get install -qy \
    mysql-client \
    memcached \
    mysql-client \
    curl \
    wget \
    libcurl4-gnutls-dev \
    libmcrypt-dev \
    libpng12-dev \
    libxml2-dev \
    libxslt-dev

# ]]
# ------------------------------------------------------------------------------
# -> 3. Install PHP extensions [[
# ------------------------------------------------------------------------------

RUN apt-get update && docker-php-ext-install curl \
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

# ]]
# ------------------------------------------------------------------------------
# -> 4. Install Xdebug [[
# ------------------------------------------------------------------------------

RUN yes | pecl install xdebug

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

RUN curl -o magerun https://raw.githubusercontent.com/netz98/n98-magerun/master/n98-magerun.phar && \
    chmod +x ./magerun && \
    mv ./magerun /usr/local/bin/

# ]]
# ------------------------------------------------------------------------------
# -> 7. Configure [[
# ------------------------------------------------------------------------------

COPY php.ini /usr/local/etc/php/php.ini

# ]]
# ------------------------------------------------------------------------------
