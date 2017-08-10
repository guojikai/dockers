FROM alpine:3.6

COPY etc /etc

# add USTC mirrors
RUN echo -e "http://mirrors.ustc.edu.cn/alpine/v3.6/main/\nhttp://mirrors.ustc.edu.cn/alpine/v3.6/community/" > /etc/apk/repositories \
    && apk update \
    && apk add \
        # enhancement
        tzdata \
        bash \
        man \
        # development dependencys
        git \
        wget \
        curl \
        # build dependencys
        ca-certificates \
        openssl \
        libcurl \
        libmcrypt-dev \
        freetype-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        libmemcached-dev \
        librdkafka-dev \
        # sets: timezone
    # set timezone
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone \
    && apk del tzdata && rm -rf /var/cache/apk/*

CMD ["/bin/bash", "-l"]

