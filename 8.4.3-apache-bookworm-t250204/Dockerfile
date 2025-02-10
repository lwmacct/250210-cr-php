FROM php:8.4.3-apache-bookworm
LABEL maintainer="https://yuque.com/lwmacct"
ARG DEBIAN_FRONTEND=noninteractive

RUN set -eux; \
    echo "配置源"; \
    sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list.d/debian.sources; \
    apt-get update && apt-get install -y --no-install-recommends ca-certificates netbase curl wget; \
    sed -i 's/http:/https:/g' /etc/apt/sources.list.d/debian.sources; \
    apt-get upgrade -y; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*;

RUN apt-get update && apt-get install -y \
        libzip-dev \
        unzip \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

LABEL org.opencontainers.image.source=https://github.com/lwmacct/250210-cr-php
LABEL org.opencontainers.image.description="lwmacct"
LABEL org.opencontainers.image.licenses=MIT
