############################################
# Dockerfile for udata system dependencies #
############################################

FROM debian:stretch-slim

# File Author / Maintainer
MAINTAINER Open Data Team

ENV DEBIAN_FRONTEND noninteractive

# Install uData system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
# Essential Tools
    tar git wget curl build-essential pkg-config ca-certificates\
# Locales management
    locales \
# Pillow
    libjpeg-dev zlib1g-dev libpng-dev libtiff5-dev libfreetype6-dev \
    liblcms2-dev libopenjp2-7-dev libwebp-dev \
# lxml dependencies
    libxml2-dev libxslt1-dev \
# Misc dependencies
    liblzma-dev libyaml-dev libffi-dev libexpat1-dev libssl1.1 mime-support \
    libmpdec2 libreadline7 libsqlite3-0 \
# Clean up
    && apt-get autoremove\
    && apt-get clean\
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Python 3.6
RUN /bin/bash -c "wget \
    https://github.com/chriskuehl/python3.6-debian-stretch/releases/download/v3.6.3-1-deb9u1/{python3.6_3.6.3-1.deb9u1_amd64,python3.6-minimal_3.6.3-1.deb9u1_amd64,python3.6-dev_3.6.3-1.deb9u1_amd64,libpython3.6_3.6.3-1.deb9u1_amd64,libpython3.6-minimal_3.6.3-1.deb9u1_amd64,libpython3.6-stdlib_3.6.3-1.deb9u1_amd64,libpython3.6-dev_3.6.3-1.deb9u1_amd64}.deb" \
    && dpkg -i *.deb \
    && rm *.deb

# Set LOCALE to UTF8
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
    && locale-gen en_US.UTF-8 \
    && dpkg-reconfigure locales \
    && /usr/sbin/update-locale LANG=en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV PYTHONIOENCODING UTF-8

# Install libpngquant for better images quantization
ENV LIBIMAGEQUANT_VERSION 2.11.4
RUN git clone https://github.com/ImageOptim/libimagequant \
    && cd libimagequant \
    && git checkout $LIBIMAGEQUANT_VERSION \
    && make shared\
    && mv libimagequant.so* /usr/local/lib \
    && cp libimagequant.h /usr/local/include \
    && cd .. \
    && rm -fr libimagequant \
    && ldconfig

# Upgrade to latest pip version
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN python3.6 get-pip.py
RUN pip3 install -U pip setuptools six
