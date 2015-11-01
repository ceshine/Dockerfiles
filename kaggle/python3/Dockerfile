FROM ceshine/py3-datascience-toolbox:latest

# MAINTAINER CeShine Lee ceshine@ceshine.net

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y byobu

# Install some tools
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y p7zip emacs

RUN DEBIAN_FRONTEND=noninteractive pip3 install git+https://github.com/quantopian/qgrid

# Temporary fix the xgboost installation problem
RUN cp /usr/local/src/xgboost/wrapper/libxgboostwrapper.so /usr/local/lib/python3.4/dist-packages/xgboost-0.4-py3.4.egg/xgboost/

# Add drive binary
ADD drive /usr/local/bin/drive

CMD byobu
