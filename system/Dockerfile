############################################
# Dockerfile for udata system dependencies #
############################################

FROM python:3.7-alpine

# Optionnal build arguments
ARG REVISION="N/A"
ARG CREATED="Undefined"

# OCI annotations
# See: https://github.com/opencontainers/image-spec/blob/master/annotations.md
LABEL "org.opencontainers.image.title"="udata system"
LABEL "org.opencontainers.image.description"="Base system dependencies for udata 2"
LABEL "org.opencontainers.image.authors"="Open Data Team"
LABEL "org.opencontainers.image.sources"="https://github.com/opendatateam/udata-dockers/tree/2-alpine/system"
LABEL "org.opencontainers.image.revision"=$REVISION
LABEL "org.opencontainers.image.created"=$CREATED

# Add Edge and bleeding repos
RUN echo -e '@edge http://dl-cdn.alpinelinux.org/alpine/edge/main' >> /etc/apk/repositories \
    && echo -e '@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories

# Install permanent system depdencies
RUN apk add --update --no-cache \
    bash \
    build-base \
    ca-certificates \
    curl \
    gettext \
    libffi-dev \
    libimagequant-dev@testing \
    libjpeg-turbo-dev \
    libpng-dev \
    libressl-dev \
    libwebp-dev \
    libxml2-dev \
    libxslt-dev \
    linux-headers \
    tiff-dev \
    yaml-dev \
    zlib-dev \
    && pip install --upgrade pip setuptools virtualenv \
    && rm -r /root/.cache
