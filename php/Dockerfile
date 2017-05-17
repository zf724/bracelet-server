FROM docker.io/php:7.1.5-alpine
MAINTAINER PHP Docker Maintainers

RUN docker-php-source extract \
    && docker-php-ext-install mysqli \
    && docker-php-source delete

ENV VERSION v1.0

ADD https://github.com/zf724/bracelet-web/archive/${VERSION}.tar.gz /var/www/

WORKDIR /var/www
RUN tar zxf /var/www/${VERSION}.tar.gz \
    && mv ${VERSION}/* . \
    && rm ${VERSION}* -rf \
    && chown -R nobody:nogroup /var/www \
    && chmod -R 777 firmware

ADD https://raw.githubusercontent.com/zf724/bracelet-server/master/php/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

VOLUME /var/www
EXPOSE 80

ENTRYPOINT ["/entrypoint.sh"]
