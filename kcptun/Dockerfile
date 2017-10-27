FROM ubuntu:16.04
MAINTAINER CeShine Lee <ceshine@ceshine.net>

RUN  apt-get update \
  && apt-get install -y wget \
  && rm -rf /var/lib/apt/lists/*

RUN cd /tmp && \
    wget https://github.com/xtaci/kcptun/releases/download/v20171021/kcptun-linux-amd64-20171021.tar.gz && \
    tar zxvf kcptun-linux-amd64-20171021.tar.gz && \
    mv server_linux_amd64 /usr/local/bin/kcpserver && \
    mv client_linux_amd64 /usr/local/bin/kcpclient
