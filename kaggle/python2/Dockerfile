FROM ceshine/py2-datascience-toolbox:latest

# MAINTAINER CeShine Lee ceshine@ceshine.net

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y byobu

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libxml2-dev libxslt1-dev lib32z1-dev

RUN pip install kaggle-cli

CMD byobu