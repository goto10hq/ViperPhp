FROM php:7.4.15-apache

RUN apt-get update && \
    apt-get install -y libpng-dev && \
    apt-get install -y libjpeg62-turbo-dev && \
    apt-get install -y libfreetype6-dev && \
    apt-get install -y libzip-dev && \
    apt-get install -y libsqlite3-dev && \
    apt-get install -y libsqlite3-0

ENV NODE_VERSION 15.8.0
ENV NODE_DOWNLOAD_SHA c2b073c4421e62aa71f0cef929e61a3334853ab211119f8ea7601612c43cd71d
RUN curl -SL "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz" --output nodejs.tar.gz \
    && echo "$NODE_DOWNLOAD_SHA nodejs.tar.gz" | sha256sum -c - \
    && tar -xzf "nodejs.tar.gz" -C /usr/local --strip-components=1 \
    && rm nodejs.tar.gz \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs

RUN npm i npm@latest -g

RUN docker-php-ext-configure gd --with-jpeg=/usr/include/ --with-freetype=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pdo_sqlite

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
