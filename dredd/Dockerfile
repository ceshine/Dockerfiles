# AppDB Core Components
#
# VERSION               0.2.0

FROM python:3.5.2
MAINTAINER CeShine Lee <lishixuan@baiwang.com>

LABEL Description="Python Base Image with Dredd installed for CI use" Vendor="Baiwang" Version="0.2.0"

# Install Nodejs, npm ,and Dredd
RUN wget https://nodejs.org/dist/v6.10.0/node-v6.10.0-linux-x64.tar.xz && \
    tar Jxf node-v6.10.0-linux-x64.tar.xz && \
    mv node-v6.10.0-linux-x64 /usr/local/nodejs
ENV PATH $PATH:/usr/local/nodejs/bin
RUN npm install -g dredd
