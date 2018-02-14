FROM guojikai/alpine:3.6-dev

USER root

# ENV HOME /root
# ENV NVM_DIR $HOME/.nvm

# ENV VERSION=v4.8.4 NPM_VERSION=2
# ENV VERSION=v6.11.2 NPM_VERSION=3
ENV VERSION=v8.1.4 \
    NPM_VERSION=5

# For base builds
# ENV CONFIG_FLAGS="--fully-static --without-npm" DEL_PKGS="libstdc++" RM_DIRS=/usr/include

RUN apk update \
    && apk add curl make gcc g++ python linux-headers binutils-gold gnupg libstdc++ yarn \
    && curl -sSLO https://nodejs.org/dist/${VERSION}/node-${VERSION}.tar.xz \
    && tar -xf node-${VERSION}.tar.xz \
    && cd node-${VERSION} \
    && ./configure --prefix=/usr ${CONFIG_FLAGS} \
    && make -j$(getconf _NPROCESSORS_ONLN) && make install \
    && cd / \
    && apk del curl make gcc g++ python linux-headers binutils-gold gnupg ${DEL_PKGS} \
    && rm -rf ${RM_DIRS} /node-${VERSION}* /usr/share/man /tmp/* /var/cache/apk/* \
    /root/.npm /root/.node-gyp /root/.gnupg /usr/lib/node_modules/npm/man \
    /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html /usr/lib/node_modules/npm/scripts
