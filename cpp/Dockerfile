FROM debian:jessie

MAINTAINER zhongwei.lzw <zhongwei.lzw@alibaba-inc.com>

RUN apt-get update && apt-get install -y \
    build-essential libevent-dev pdftk  && \
    apt-get clean && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/*
