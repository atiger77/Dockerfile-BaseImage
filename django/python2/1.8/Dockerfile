FROM python:2.7-slim

MAINTAINER zhongwei.lzw <zhongwei.lzw@alibaba-inc.com>

RUN apt-get update && apt-get install -y \
		gcc \
		gettext \
		mysql-client libmysqlclient-dev \
	--no-install-recommends && rm -rf /var/lib/apt/lists/*

ENV DJANGO_VERSION 1.8.2

ADD pip.conf /root/.pip/pip.conf
RUN pip install mysqlclient django=="$DJANGO_VERSION"
