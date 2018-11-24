#
# Use build context ../ !!!!
#

FROM arm32v6/php:7-fpm-alpine

WORKDIR /var/www

COPY qemu-arm-static /usr/bin/qemu-arm-static

RUN apk update
RUN apk add zlib zlib-dev
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo_mysql

COPY ./gbridge-src/web/ /var/www/
COPY ./docker-web-fpm/laravel-dotenv /var/www/.env

RUN chown -R www-data:www-data /var/www/
RUN chmod -R 777 /var/www/storage/

ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && ln -s $(composer config --global home) /root/composer
ENV PATH $PATH:/root/composer/vendor/bin7

ARG GITHUB_API_TOKEN
RUN su -s /bin/bash -c "composer config -g github-oauth.github.com '${GITHUB_API_TOKEN}'" www-data
RUN su -s /bin/bash -c "composer install" www-data
RUN su -s /bin/bash -c "composer update" www-data
RUN su -s /bin/bash -c "rm /var/www/.composer/auth.json" www-data
