FROM ceshine/py3-datascience-toolbox:latest

# MAINTAINER CeShine Lee ceshine@ceshine.net

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y byobu

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libxml2-dev libxslt1-dev lib32z1-dev

RUN pip3 install kaggle-cli

CMD byobu
