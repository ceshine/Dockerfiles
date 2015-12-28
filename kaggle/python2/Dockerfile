FROM ceshine/py2-datascience-toolbox:latest

# MAINTAINER CeShine Lee ceshine@ceshine.net

# RUN sed -i 's/http:\/\/archive.ubuntu.com/http:\/\/mirror.internode.on.net\/pub\/ubuntu/g' /etc/apt/sources.list

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y byobu

RUN DEBIAN_FRONTEND=noninteractive pip install git+https://github.com/quantopian/qgrid

# Get rid of InsecurePlatformWarning
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libffi-dev libssl-dev
RUN pip install pyopenssl ndg-httpsclient pyasn1


# Add drive binary
ADD drive /usr/local/bin/drive

CMD byobu
