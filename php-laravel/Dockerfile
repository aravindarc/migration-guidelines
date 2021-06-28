FROM aravindbootlabs/php-apache-alpine:php-7.2.3_apache-2_alpine-3.7

RUN set -xe; \
    apk add --update --no-cache --virtual .temp-deps \
        autoconf \
        gcc \
        make \
        g++ \
        pcre-dev \
        libzip-dev \
        libjpeg-turbo-dev \
        libwebp-dev \
        libxpm-dev \
        libpng-dev \
        freetype-dev \
        zlib-dev; \
    apk add --update --no-cache --virtual .perm-deps \
        libpng \
        freetype \
        libzip \
        pcre \
        libwebp \
        libxpm \
        libjpeg-turbo; \
    docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/; \
    docker-php-ext-install pdo_mysql gd mbstring zip exif pcntl mysqli calendar; \
    apk del .temp-deps;

RUN mkdir /var/www/html

COPY --chown=apache:apache . /var/www/html

COPY --chown=apache:apache .apache/httpd.conf /etc/apache2/httpd.conf

ENTRYPOINT ["docker-php-entrypoint"]

CMD ["/usr/local/bin/apache2-foreground"]
