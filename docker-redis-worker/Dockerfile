#
# Use build context ../ !!!!
#

FROM arm32v6/node:8-alpine
WORKDIR /usr/src/gbridge-redis-worker

COPY qemu-arm-static /usr/bin/qemu-arm-static

COPY ./gbridge-src/redis-worker/package*.json ./
RUN npm install

COPY ./gbridge-src/redis-worker/ ./
COPY ./gbridge-src/redis-worker/config.sample.js ./config.js

ENTRYPOINT [ "npm" ]
CMD [ "start" ]
