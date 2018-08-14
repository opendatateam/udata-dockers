###############################################
# Dockerfile for udata builds on CircleCI 2.0 #
###############################################

FROM udata/system:2-alpine

# Optionnal build arguments
ARG REVISION="N/A"
ARG CREATED="Undefined"

# OCI annotations
# See: https://github.com/opencontainers/image-spec/blob/master/annotations.md
LABEL "org.opencontainers.image.title"="udata CircleCI"
LABEL "org.opencontainers.image.description"="udata build environment for CircleCI 2.0"
LABEL "org.opencontainers.image.authors"="Open Data Team"
LABEL "org.opencontainers.image.sources"="https://github.com/opendatateam/udata-dockers/tree/master/circleci"
LABEL "org.opencontainers.image.revision"=$REVISION
LABEL "org.opencontainers.image.created"=$CREATED

# Install docker system dependencies
RUN apk add --no-cache \
# CircleCI requirements
    gzip openssh-client openssh-server \
# PhantomJS requirements
    fontconfig-dev \
# Other tools
    jq dockerize@testing

COPY .bashrc /root/

ENV NVM_DIR /root/.nvm
ENV NVM_VERSION 0.33.4
# NVM is failing with -e option
RUN echo '\n# Failsafe NVM activation\nset +e' >> /root/.bashrc
RUN curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v${NVM_VERSION}/install.sh | bash
RUN echo '\nset -e' >> /root/.bashrc

# Upgrade to latest virtualenv version
RUN pip3 install -U virtualenv
