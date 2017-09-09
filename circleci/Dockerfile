###############################################
# Dockerfile for udata builds on CircleCI 2.0 #
###############################################

FROM udata/system

# File Author / Maintainer
MAINTAINER Open Data Team

# Install docker system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
# Docker (required for extra repository)
    apt-transport-https ca-certificates gnupg2 software-properties-common \
# CircleCI requirements
    openssh-client openssh-server gzip \
# Clean up
    && apt-get autoremove\
    && apt-get clean\
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Add Docker gpg key
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -

# Add Docker repository
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

# Install Docker
RUN apt-get update && apt-get install -y --no-install-recommends docker-ce \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV DOCKER_COMPOSE_VERSION 1.16.1

# Install Docker Compose
RUN curl -L https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-`uname -s`-`uname -m` \
    > /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose

# Substituting sh for bash here to use `source`. Beware - your build times could be
# longer if you are doing shell-intensive tasks!
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# We're just setting it to the root user's home (root is default on docker)
# though you could set it to your' user's home if you need a non-root user
ENV NVM_DIR=/root/.nvm
ENV NVM_VERSION=0.33.4
RUN wget -qO- https://raw.githubusercontent.com/creationix/nvm/v${NVM_VERSION}/install.sh | bash

# Upgrade to latest virtualenv version
RUN pip install -U virtualenv
