# vim: set foldmarker=[[,]] foldlevel=0 foldmethod=marker spell:
# ------------------------------------------------------------------------------
# -> 1. Base image [[
# ------------------------------------------------------------------------------

FROM php:5.6-fpm-alpine

# ]]
# ------------------------------------------------------------------------------
# -> 2. Install base packages [[
# ------------------------------------------------------------------------------

RUN apk add --no-cache \
    wget \
    ssmtp \
    autoconf \
    build-base \
    libxml2-dev \
    libmcrypt-dev

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

# ]]
# ------------------------------------------------------------------------------
# -> 4. Install Xdebug [[
# ------------------------------------------------------------------------------

ENV XDEBUG_VERSION 2.3.3
RUN wget http://xdebug.org/files/xdebug-$XDEBUG_VERSION.tgz \
    && tar -zxvf xdebug-$XDEBUG_VERSION.tgz && cd xdebug-$XDEBUG_VERSION \
    && phpize && ./configure --enable-xdebug && make && make install

# ]]
# ------------------------------------------------------------------------------
# -> 5. Magerun [[
# ------------------------------------------------------------------------------

RUN curl -o magerun https://raw.githubusercontent.com/netz98/n98-magerun/master/n98-magerun.phar && \
    chmod +x ./magerun && \
    mv ./magerun /usr/local/bin/

# ]]
# ------------------------------------------------------------------------------
# -> 6. Configure [[
# ------------------------------------------------------------------------------

COPY php.ini /usr/local/etc/php/php.ini
COPY ssmtp.conf /etc/ssmtp/ssmtp.conf

# ]]
# ------------------------------------------------------------------------------
