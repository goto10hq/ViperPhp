FROM php:7.3-apache

RUN apt-get update && \
    apt-get install -y libpng-dev && \
    apt-get install -y libjpeg62-turbo-dev && \
    apt-get install -y libfreetype6-dev && \
    apt-get install -y libzip-dev

ENV NODE_VERSION 11.1.0
ENV NODE_DOWNLOAD_SHA 52289a646a27511f5808290357798c7ebd4b5132a8fc3bf7d5bf53183b89c668
RUN curl -SL "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz" --output nodejs.tar.gz \
    && echo "$NODE_DOWNLOAD_SHA nodejs.tar.gz" | sha256sum -c - \
    && tar -xzf "nodejs.tar.gz" -C /usr/local --strip-components=1 \
    && rm nodejs.tar.gz \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs

RUN npm i npm@latest -g

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo_mysql

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
