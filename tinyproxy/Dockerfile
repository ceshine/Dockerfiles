# Based on https://github.com/monokal/docker-tinyproxy

FROM ubuntu:16.04
MAINTAINER CeShine Lee <ceshine@ceshine.net>

RUN  apt-get update \
  && apt-get install -y tinyproxy \
  && rm -rf /var/lib/apt/lists/*

ADD run.sh /opt/docker-tinyproxy/run.sh

EXPOSE 8888
ENTRYPOINT ["/opt/docker-tinyproxy/run.sh"]
