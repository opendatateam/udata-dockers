############################################
# Dockerfile for udata system dependencies #
############################################

FROM debian:jessie

# File Author / Maintainer
MAINTAINER Open Data Team

# Install uData system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    # Essential Tools
    tar git wget curl build-essential pkg-config \
    # Python tools
    python python-dev python-pip\
    # Pillow
    libjpeg-dev zlib1g-dev libpng12-dev libtiff5-dev libfreetype6-dev \
    liblcms2-dev libopenjpeg-dev libwebp-dev libpng12-dev \
    # lxml dependencies
    libxml2-dev libxslt1-dev \
    # Misc dependencies
    liblzma-dev libyaml-dev libffi-dev \
    # Clean up
    && apt-get autoremove\
    && apt-get clean\
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install libpngquant for better images quantization
ENV LIBIMAGEQUANT_VERSION 2.9.1
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
RUN pip install -U pip setuptools six
