FROM debian:jessie

MAINTAINER zhongwei.lzw <zhongwei.lzw@alibaba-inc.com>

# disable interactive functions
ENV DEBIAN_FRONTEND noninteractive

# set default java environment variable
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

RUN apt-get update && \
    apt-get install -y --no-install-recommends openjdk-7-jdk curl && \
    rm -rf /var/lib/apt/lists/*

ENV MAVEN_VERSION 3.2.5

RUN mkdir -p /usr/share/maven \
  && curl -fsSL http://apache.osuosl.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
    | tar -xzC /usr/share/maven --strip-components=1 \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME /usr/share/maven

VOLUME /root/.m2
