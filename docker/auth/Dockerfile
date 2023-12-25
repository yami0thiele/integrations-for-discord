FROM php:8.3-fpm

RUN useradd -m -s /bin/sh -u 1000 nginx

RUN apt-get update && \
    apt-get install -y git gnupg2 zip

COPY ./docker/auth/www.conf /usr/local/etc/php-fpm.d/zzz-www.conf
COPY --from=composer /usr/bin/composer /usr/bin/composer

USER nginx
