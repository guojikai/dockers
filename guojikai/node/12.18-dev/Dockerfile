FROM node:12.18-stretch-slim

ENV DEV_SOFTS \
    inetutils-ping \
    procps \
    wget \
    vim \
    python

COPY sources.list /usr/src/sources.list.mirror

RUN echo "Build start..." \
    && echo "Change sources to Mirror in China..." \
    && mv /etc/apt/sources.list /usr/src/sources.list.backup \
    && cp /usr/src/sources.list.mirror /etc/apt/sources.list \
    && apt-get update \
    && echo "Install dev softs..." \
    && apt-get install -y $DEV_SOFTS \
    && echo "Install npm mirrors..." \
    && npm install -g cnpm --registry=https://registry.npm.taobao.org \
    && npm install -g tyarn --registry=https://registry.npm.taobao.org \
    && echo "Install nodejs tools..." \
    && npm install -g pm2