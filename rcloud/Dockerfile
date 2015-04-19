FROM ubuntu:14.04

MAINTAINER CeShine <ceshine@ceshine.net>

RUN apt-get update && apt-get dist-upgrade -y

# System Dependencies
RUN apt-get install -y libxt-dev libcurl4-openssl-dev libcairo2-dev

# Install R
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
RUN echo 'deb http://cran.rstudio.com/bin/linux/ubuntu trusty/' >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y r-base-dev

# Create Rcloud directory
RUN mkdir /rcloud
WORKDIR /rcloud

# Clone Rcloud codebase
RUN apt-get install -y git-core
RUN cd /tmp && git clone https://github.com/att/rcloud.git && mv rcloud/* /rcloud/
ADD rcloud.conf /rcloud/conf/rcloud.conf

# Set up locale 
RUN locale-gen en_US.UTF-8  
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  

RUN ./scripts/bootstrapR.sh
RUN apt-get install -y redis-server

EXPOSE 8080
CMD service redis-server start && ./scripts/fresh_start.sh