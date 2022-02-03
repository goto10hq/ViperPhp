FROM php:8.1.2-apache

RUN apt-get update && \
    apt-get install -y libpng-dev && \
    apt-get install -y libjpeg62-turbo-dev && \
    apt-get install -y libfreetype6-dev && \
    apt-get install -y libzip-dev && \
    apt-get install -y libsqlite3-dev && \
    apt-get install -y libsqlite3-0 && \
    apt-get install -y nodejs && \
    apt-get install -y npm

RUN npm i npm@latest -g

RUN docker-php-ext-configure gd --with-jpeg=/usr/include/ --with-freetype=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pdo_sqlite

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
