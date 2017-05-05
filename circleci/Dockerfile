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

# Install Docker Compose
RUN curl -L https://github.com/docker/compose/releases/download/1.13.0/docker-compose-`uname -s`-`uname -m` \
    > /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose
