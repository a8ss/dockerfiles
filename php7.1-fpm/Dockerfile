# 安装扩展： gd(freetype,gif,jpeg,png) pdo_mysql
# 生成/usr/local/etc/php.ini文件，并修改其中值：
#   expose_php = off
#   date.timezone = PRC
# 加载opcache.so
# 更换工作目录为/apps
# 时区+8
# 支持中文
# 打开默认的bash alias
# 安装软件：vim cron

FROM php:7.1-fpm


RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        vim \
        cron \
#    && docker-php-ext-install -j$(nproc) iconv \  # 已默认安装
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd pdo_mysql \
    && rm -rf /var/lib/apt/lists/*
    
RUN set -ex \
    && mkdir /apps \
    && chown www-data.www-data /apps \
	&& cd /usr/local/etc \
    && cp php/php.ini-production php/php.ini \
    && sed -i 's/expose_php\ =\ On/expose_php\ =\ Off/' php/php.ini \
    && sed -i 's/\;date\.timezone\ =/date\.timezone\ = PRC/' php/php.ini \
    && { \
        echo 'zend_extension=opcache.so'; \
    } | tee -a php/php.ini

# OS config
ENV LANG C.UTF-8
ENV TZ=Asia/Shanghai
RUN set -ex \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \
    && sed -i 's/^#\s\(alias\|export\w\+\s\)/\1/' /root/.bashrc

WORKDIR /apps
