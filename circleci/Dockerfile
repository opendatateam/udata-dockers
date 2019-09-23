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
LABEL "org.opencontainers.image.sources"="https://github.com/opendatateam/udata-dockers/tree/2-alpine/circleci"
LABEL "org.opencontainers.image.revision"=$REVISION
LABEL "org.opencontainers.image.created"=$CREATED

# Install docker system dependencies
RUN apk add --no-cache \
# CircleCI requirements
    git gzip openssh-client openssh-server \
# Other tools
    jq dockerize@testing

COPY .bashrc /root/
