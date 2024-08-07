FROM debian:jessie

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r redis && useradd -r -g redis redis

ENV REDIS_VERSION 3.0.7
ENV REDIS_DOWNLOAD_URL http://download.redis.io/releases/redis-3.0.7.tar.gz
ENV REDIS_DOWNLOAD_SHA e56b4b7e033ae8dbf311f9191cf6fdf3ae974d1c

ENV FETCH_DEPS \
    ca-certificates

RUN set -ex; \
    apt-get update; \
    apt-get install -y --no-install-recommends $FETCH_DEPS; \
    rm -rf /var/lib/apt/lists/*; \
    \
    dpkgArch="$(dpkg --print-architecture | awk -F- '{ print $NF }')"; \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4; \
    apt-get purge -y --auto-remove $FETCH_DEPS

ENV BUILD_DEPS \
    wget \
    gcc \
    make \
    libc6-dev

RUN set -ex; \
    apt-get update; \
    apt-get install -y --no-install-recommends $BUILD_DEPS; \
    rm -rf /var/lib/apt/lists/*; \
    \
    wget -O redis.tar.gz "$REDIS_DOWNLOAD_URL"; \
    echo "$REDIS_DOWNLOAD_SHA *redis.tar.gz" | sha1sum -c -; \
    mkdir -p /usr/src/redis; \
    tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1; \
    rm redis.tar.gz; \
    \
    make -C /usr/src/redis -j "$(nproc)"; \
    make -C /usr/src/redis install; \
    \
    rm -r /usr/src/redis; \
    \
    apt-get purge -y --auto-remove $BUILD_DEPS

RUN mkdir -p /data/redis \
    && chown redis:redis /data/redis
WORKDIR /data/redis

EXPOSE 6379
CMD ["redis-server", "/usr/local/etc/redis/redis.conf"]
