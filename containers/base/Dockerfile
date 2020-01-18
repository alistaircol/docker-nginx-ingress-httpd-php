FROM php:7.3-apache
# Best practice apparently to do this
RUN rm -rf /var/lib/apt/lists/partial && rm -rf /var/lib/apt/lists/*

# install some essential stuff, mostly for composer and general utilities for managing apps
RUN apt-get update  -o Acquire::BrokenProxy="true" -o Acquire::http::No-Cache="true" -o Acquire::http::Pipeline-Depth="0" --fix-missing
RUN apt-get install -o Acquire::BrokenProxy="true" -o Acquire::http::No-Cache="true" -o Acquire::http::Pipeline-Depth="0" -y \
    apt-utils \
    bash-completion \
    zip \
    unzip \
    apt-utils \
    nano \
    curl \
    pv \
    git \
    libzip-dev \
    zlibc \
    zlib1g \
    libmemcached-dev \
    netcat \
    libmagickwand-dev \
    jq

# install php extensions
RUN docker-php-ext-configure zip --with-libzip
RUN docker-php-ext-install zip

RUN pecl install \
    igbinary-3.0.1 \
    msgpack-2.0.3 \
    imagick-3.4.4 \
    memcached-3.1.3 \
    xdebug-2.7.2

RUN docker-php-ext-enable \
    memcached \
    imagick \
    xdebug

RUN docker-php-ext-install \
    pdo \
    pdo_mysql

RUN . /etc/apache2/envvars
RUN a2enmod rewrite
RUN a2enmod proxy_http
RUN usermod -u 1000 www-data

# https://github.com/docker-library/php/issues/344#issuecomment-364843883
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
COPY --from=docker:latest /usr/local/bin/docker /usr/local/bin/docker

# some aliases and composer autocomplete
# COPY ./.bashrc /var/www/.bashrc

# make composer complain less
RUN mkdir -p /var/www/.composer; chown -R 1000:1000 /var/www/.composer
