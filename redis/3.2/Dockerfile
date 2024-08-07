FROM guojikai/alpine:3.6-dev

RUN apk update \
    && apk add \
        ca-certificates \
        redis \
    && mkdir -p /data/redis \

WORKDIR /data/redis

EXPOSE 6379

CMD ["redis-server", "/etc/redis/redis.conf"]

