FROM guojikai/alpine:3.6-dev

USER root

ENV HOME /root
ENV NVM_DIR $HOME/.nvm
ENV NODE_VERSION v6.10.3


RUN apk update \
    # install yarn
    && apk add yarn \
    # install nvm
    && touch /root/.profile && touch /root/.bashrc  && touch /root/.bash_profile \
    # && curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
    && git clone https://github.com/creationix/nvm.git $NVM_DIR && cd $NVM_DIR \
    && touch $NVM_DIR/.nvmrc \
    && git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" origin`
    # && . "$NVM_DIR/nvm.sh"

