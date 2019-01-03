FROM php:7.0-fpm-alpine
RUN sed -i 's/^http:\/\/dl-cdn\.alpinelinux\.org\//https:\/\/mirrors\.aliyun\.com\//' /etc/apk/repositories \
    && apk add libwebp-dev libpng-dev jpeg-dev freetype freetype-dev \
    && docker-php-ext-configure gd --with-webp-dir=/usr/incloud/ --with-jpeg-dir=/usr/incloud/ --with-png-dir=/usr/incloud/ --with-freetype-dir=/usr/incloud/ \
    && docker-php-ext-install pdo_mysql gd \
    && cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini \
    && echo 'zend_extension=opcache.so' >> /usr/local/etc/php/php.ini \ 
