FROM ubuntu:14.04

MAINTAINER CeShine <ceshine@ceshine.net>

RUN apt-get update && apt-get dist-upgrade -y

# Install R
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
RUN echo 'deb http://cran.rstudio.com/bin/linux/ubuntu trusty/' >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y r-base-dev

# Create Rcloud directory
RUN mkdir /src
WORKDIR /src

CMD bash -c "R"