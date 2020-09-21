FROM php:7.4-fpm-buster

#composerをインストール
COPY --from=composer:1.10 /usr/bin/composer /usr/bin/composer

#npmインストール
COPY --from=node:10.22 /usr/local/bin /usr/local/bin
COPY --from=node:10.22 /usr/local/lib /usr/local/lib

RUN apt-get update \
&& apt-get install -y \
git \
zip \
unzip \
vim \
libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
&& docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
&& docker-php-ext-install pdo_mysql bcmath -j$(nproc) gd 

COPY php.ini /usr/local/etc/php/ 

WORKDIR /var/www/html