FROM ceshine/py2-datascience-toolbox:latest

# MAINTAINER CeShine Lee ceshine@ceshine.net

# RUN sed -i 's/http:\/\/archive.ubuntu.com/http:\/\/mirror.internode.on.net\/pub\/ubuntu/g' /etc/apt/sources.list

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y byobu

CMD byobu