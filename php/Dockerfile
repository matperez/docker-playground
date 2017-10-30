FROM php:7.1-fpm-alpine
RUN apk apk update \
    && apk add --no-cache libmcrypt libmcrypt-dev libpng-dev git mercurial zip unzip sqlite-dev \
        icu-dev icu-libs icu libedit-dev libjpeg-turbo-dev freetype-dev libxml2-dev \
        gcc g++ make autoconf curl
RUN apk add bash bash-completion mc
RUN docker-php-ext-install -j$(getconf _NPROCESSORS_ONLN) iconv mcrypt mysqli pdo pdo_mysql pdo_sqlite \
    intl json readline soap xml xmlrpc zip
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(getconf _NPROCESSORS_ONLN) gd
RUN pecl install xdebug redis && docker-php-ext-enable xdebug redis \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port=9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_host=dockerhost" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && rm -rf /tmp/*
