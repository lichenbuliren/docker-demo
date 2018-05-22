FROM php:5.6-fpm

ADD sources.list    /etc/apt/sources.list

#COPY redis.tgz /home/redis.tgz
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mysql mysqli pdo_mysql

#RUN pecl install /home/redis.tgz && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini

RUN apt-get install -y \
    && pecl install redis && docker-php-ext-enable redis \
    && docker-php-source delete \
    && apt-get clean; rm -r /var/lib/apt/lists/* /tmp/*

ADD php.ini    /usr/local/etc/php/php.ini
ADD php-fpm.conf    /usr/local/etc/php-fpm.conf

WORKDIR /opt
RUN usermod -u 1000 www-data

EXPOSE 9000
VOLUME ["/opt"]