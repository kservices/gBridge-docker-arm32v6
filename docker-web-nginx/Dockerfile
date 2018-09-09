#
# Use build context ../ !!!!
#

FROM arm32v6/nginx:1.15-alpine

WORKDIR /var/www/html/

COPY qemu-arm-static /usr/bin/qemu-arm-static

COPY ./docker-web-nginx/vhost.conf /etc/nginx/conf.d/default.conf

RUN chown -R www-data:www-data /var/www/