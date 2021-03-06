ARG BUILD_VERSION
FROM arm32v7/debian:${BUILD_VERSION}-slim

# QEMU for crossbuilds
COPY qemu-arm-static /usr/bin/qemu-arm-static

# Default ENV
ENV LANG C.UTF-8
ENV DEBIAN_FRONTEND noninteractive
ENV CURL_CA_BUNDLE /etc/ssl/certs/ca-certificates.crt

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Base system
ARG BASHIO_VERSION=0.7.0
RUN apt-get update && apt-get install -y --no-install-recommends \
        bash \
        jq \
        tzdata \
        curl \
        ca-certificates \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir -p /usr/share/man/man1 \
    \
    && mkdir -p /tmp/bashio \
    && curl -L -s https://github.com/hassio-addons/bashio/archive/v${BASHIO_VERSION}.tar.gz | tar -xzf - --strip 1 -C /tmp/bashio \
    && mv /tmp/bashio/lib /usr/lib/bashio \
    && ln -s /usr/lib/bashio/bashio /usr/bin/bashio \
    && rm -rf /tmp/bashio
