FROM ceshine/py3-datascience-toolbox:latest

# MAINTAINER CeShine Lee ceshine@ceshine.net

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y byobu

RUN DEBIAN_FRONTEND=noninteractive pip3 install git+https://github.com/quantopian/qgrid

# Add drive binary
ADD drive /usr/local/bin/drive

CMD byobu
