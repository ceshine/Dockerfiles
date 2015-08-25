FROM ubuntu:14.04

# MAINTAINER CeShine Lee ceshine@ceshine.net

# RUN sed -i 's/http:\/\/archive.ubuntu.com/http:\/\/mirror.internode.on.net\/pub\/ubuntu/g' /etc/apt/sources.list
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y
RUN DEBIAN_FRONTEND=noninteractive locale-gen en_US en_US.UTF-8

# Install python packages
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y python3

# Install compile tools
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y python3-dev gfortran libatlas-base-dev libfreetype6-dev libxft-dev libpng-dev g++

# Install pip
RUN apt-get install -y wget
RUN wget -O /tmp/get-pip.py https://bootstrap.pypa.io/get-pip.py
RUN python3 /tmp/get-pip.py

# Install Cython
RUN pip install cython

# Install core packages
RUN DEBIAN_FRONTEND=noninteractive pip install numpy
RUN DEBIAN_FRONTEND=noninteractive pip install scipy
RUN DEBIAN_FRONTEND=noninteractive pip install matplotlib
RUN DEBIAN_FRONTEND=noninteractive pip install "ipython[all]"
RUN DEBIAN_FRONTEND=noninteractive pip install -U "pandas>0.14.0"
RUN DEBIAN_FRONTEND=noninteractive pip install -U scikit-learn

RUN DEBIAN_FRONTEND=noninteractive pip install seaborn

# Install pymc
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git-core
RUN DEBIAN_FRONTEND=noninteractive pip install -U Theano patsy
RUN DEBIAN_FRONTEND=noninteractive pip install git+https://github.com/pymc-devs/pymc3

# Install xgboost
RUN cd /usr/local/src && git clone https://github.com/dmlc/xgboost.git  && cd xgboost && sh build.sh && cd python-package && python3 setup.py install

#Setting up working directory
RUN mkdir /lab 
WORKDIR /lab

#Minimize image size
RUN (apt-get autoremove -y; \
     apt-get clean -y)

#Setting up ipython notebook server
EXPOSE 8888
CMD ipython notebook --no-browser --ip=0.0.0.0 --port 8888
