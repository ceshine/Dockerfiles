FROM ubuntu:latest

# MAINTAINER CeShine Lee ceshine@ceshine.net

# RUN sed -i 's/http:\/\/archive.ubuntu.com/http:\/\/mirror.internode.on.net\/pub\/ubuntu/g' /etc/apt/sources.list

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y
RUN DEBIAN_FRONTEND=noninteractive locale-gen en_US en_US.UTF-8

# Install pypy for occasional needs for speed boost
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y pypy

# Install git
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git-core

# Install compile tools
RUN apt-get install -y gfortran libatlas-base-dev gfortran pkg-config \
            libfreetype6-dev libxft-dev libpng-dev libhdf5-serial-dev g++ \
            make patch lib32ncurses5-dev

# Install python packages
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y python python-dev

# Install pip
RUN sudo apt-get install -y wget
RUN wget -O /tmp/get-pip.py https://bootstrap.pypa.io/get-pip.py
RUN python /tmp/get-pip.py

# Install Cython
RUN pip install cython

# Install IPython
RUN DEBIAN_FRONTEND=noninteractive pip install jupyter

# Install the core tools
RUN pip install -U  numpy scipy matplotlib
RUN pip install -U "pandas>=0.14.0"
RUN pip install -U "scikit-learn>=0.14.0"

# Install visualization tools
RUN pip install -U seaborn ggplot

# Install pymc
RUN pip install -U pydot2 tables
RUN pip install -U "pymc>=2.3"

# Install xgboost
RUN cd /usr/local/src && git clone https://github.com/dmlc/xgboost.git && cd xgboost && sh build.sh && cd python-package && python setup.py install

# Install graphviz
RUN apt-get install -y graphviz

#Setting up working directory
RUN mkdir /lab
WORKDIR /lab

#Minimize image size
RUN (apt-get autoremove -y; \
     apt-get clean -y)

#Setting up ipython notebook server
EXPOSE 8888
CMD jupyter notebook --no-browser --ip=0.0.0.0 --port 8888
