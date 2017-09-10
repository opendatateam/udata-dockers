###############################################
# Dockerfile for udata builds on CircleCI 2.0 #
###############################################

FROM udata/system

# File Author / Maintainer
MAINTAINER Open Data Team

# Install docker system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
# CircleCI requirements
    bash openssh-client openssh-server gzip ca-certificates \
# PahntomJS requirements
    libfontconfig1-dev \
# Clean up
    && apt-get autoremove\
    && apt-get clean\
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# We're just setting it to the root user's home (root is default on docker)
# though you could set it to your' user's home if you need a non-root user
ENV NVM_DIR /usr/local/nvm
ENV NVM_VERSION 0.33.4
RUN curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v${NVM_VERSION}/install.sh | bash

# Upgrade to latest virtualenv version
RUN pip install -U virtualenv
