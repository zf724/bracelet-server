FROM docker.io/php:7.1.5-apache
MAINTAINER PHP Docker Maintainers

RUN docker-php-source extract \
    && docker-php-ext-install mysqli \
    && docker-php-source delete

ENV VERSION 1.0

ADD https://github.com/zf724/bracelet-web/archive/v${VERSION}.tar.gz /var/www/html

WORKDIR /var/www/html
RUN tar zxf /var/www/html/v${VERSION}.tar.gz \
    && rm v${VERSION}.tar.gz \
    && mv bracelet-web-${VERSION}/* bracelet-web-${VERSION}/.htaccess . \
    && rm bracelet-web-${VERSION} -rf \
    && chown -R nobody:nogroup /var/www/html \
    && chmod -R 777 firmware \
    && chmod 444 .htaccess

RUN set -xe \
    && ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/ \
    && sed -i -e '/AllowOverride None/s/None/All/' /etc/apache2/apache2.conf

VOLUME /var/www/html
EXPOSE 80
