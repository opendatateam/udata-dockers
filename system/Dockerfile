############################################
# Dockerfile for udata system dependencies #
############################################

FROM python:3.7-slim-buster

# File Author / Maintainer
MAINTAINER Open Data Team

ENV DEBIAN_FRONTEND noninteractive

# Install uData system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
# Essential Tools
    tar git wget curl build-essential pkg-config \
# Locales management
    locales \
# Pillow
    libjpeg-dev zlib1g-dev libpng-dev libtiff5-dev libfreetype6-dev \
    liblcms2-dev libopenjp2-7-dev libwebp-dev libimagequant-dev \
# lxml dependencies
    libxml2-dev libxslt1-dev \
# Misc dependencies
    liblzma-dev libyaml-dev libffi-dev \
# Clean up
    && apt-get autoremove\
    && apt-get clean\
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set LOCALE to UTF8
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
    && locale-gen en_US.UTF-8 \
    && dpkg-reconfigure locales \
    && /usr/sbin/update-locale LANG=en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV PYTHONIOENCODING UTF-8

# Upgrade to latest pip version
RUN pip install -U pip setuptools
