FROM php:8.3.1RC3-fpm-bullseye
# FROM php:8.0.12-fpm-bullseye

RUN apt update && apt install zip unzip \
    && docker-php-ext-install mysqli pdo pdo_mysql \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get install zlib1g-dev libwebp-dev libfreetype6-dev libjpeg-dev libpng-dev -y \
    && docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install gd

RUN docker-php-ext-install exif

RUN apt-get install -y libmagickwand-dev --no-install-recommends && rm -rf /var/lib/apt/lists/*
RUN curl 'http://pecl.php.net/get/imagick-3.7.0.tgz' -o imagick-3.7.0.tgz \
    && pecl install imagick-3.7.0.tgz \
    && rm -rf imagick-3.7.0.tgz \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable imagick 

RUN apt update && apt install default-mysql-client -y

RUN pecl install redis && docker-php-ext-enable redis 
RUN pecl install pcov && docker-php-ext-enable pcov 

RUN apt install libcurl4-openssl-dev pkg-config libssl-dev -y
RUN pecl install mongodb && docker-php-ext-enable mongodb

RUN apt-get install -y zlib1g-dev libzip-dev \
    && docker-php-ext-install zip

RUN docker-php-ext-install bcmath