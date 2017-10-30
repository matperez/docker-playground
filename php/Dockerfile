FROM php:7.1-fpm-alpine
RUN apk apk --no-cache update \
    && apk --no-cache upgrade \
    && apk add libmcrypt libmcrypt-dev libpng-dev git mercurial zip unzip sqlite-dev \
        icu-dev icu-libs icu libedit-dev libjpeg-turbo-dev freetype-dev libxml2-dev
RUN apk add bash bash-completion mc
RUN docker-php-ext-install -j$(getconf _NPROCESSORS_ONLN) iconv mcrypt mbstring mysqli pdo pdo_mysql \
    intl json readline soap xml xmlrpc zip
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(getconf _NPROCESSORS_ONLN) gd
RUN curl -sS https://getcomposer.org/installer | php \ 
    && mv composer.phar /usr/local/bin/composer

