FROM php:5.6-apache
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        php5-mysql \
    && docker-php-ext-install -j$(nproc) iconv mcrypt mysql \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN a2enmod rewrite headers

RUN a2dissite 000-default

COPY virtualhost.conf /etc/apache2/sites-available/001-virtualhost.conf
RUN a2ensite 001-virtualhost

#RUN chown www-data:www-data /var/www/html/error.log /var/www/html/access.log