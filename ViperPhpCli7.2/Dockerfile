FROM php:7.2-cli-alpine3.8

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev

RUN docker-php-ext-install gd
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo_mysql