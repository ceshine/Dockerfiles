FROM ceshine/py3-datascience-toolbox:latest

# MAINTAINER CeShine Lee ceshine@ceshine.net

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y byobu

# Install some tools
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y p7zip emacs

RUN DEBIAN_FRONTEND=noninteractive pip3 install git+https://github.com/quantopian/qgrid

# Temporary fix the xgboost installation problem
RUN cp /usr/local/src/xgboost/wrapper/libxgboostwrapper.so /usr/local/lib/python3.4/dist-packages/xgboost-0.4-py3.4.egg/xgboost/

# Install Vowpal Wabbit
RUN apt-get update

RUN apt-get -y install libboost-all-dev zlib1g-dev wget vim gcc python-dev python-setuptools libffi-dev git-core build-essential libtool automake wget

RUN wget https://github.com/JohnLangford/vowpal_wabbit/archive/7.10.tar.gz
RUN tar zxvf 7.10.tar.gz && mv vowpal_wabbit-7.10 / && cd /vowpal_wabbit-7.10 && ./autogen.sh && make && make install

RUN ln -s /vowpal_wabbit-7.10 /vowpal_wabbit

ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/lib

# Add drive binary
ADD drive /usr/local/bin/drive

CMD byobu
