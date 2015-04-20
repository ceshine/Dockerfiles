FROM ubuntu:latest

# MAINTAINER CeShine Lee ceshine@ceshine.net

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y
RUN DEBIAN_FRONTEND=noninteractive locale-gen en_US en_US.UTF-8

# Install pypy for ocassional needs for speed boosts
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y pypy

# Install git
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git-core

# Install python packages
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y python python-pip\ 
                    python-numpy python-scipy python-matplotlib

# Install Pandas and ScikitLearn
RUN pip install "pandas>=0.14.0"
RUN pip install "scikit-learn>=0.14.0"

# Need to update ipython or ipython notebook will crash
RUN DEBIAN_FRONTEND=noninteractive pip install "ipython[all]" --upgrade
RUN DEBIAN_FRONTEND=noninteractive pip install "tornado>=4.0"

#Setting up working directory
RUN mkdir /lab 
WORKDIR /lab

#Minimize image size
RUN (apt-get autoremove -y; \
     apt-get clean -y)

#Setting up ipython notebook server
EXPOSE 8888
CMD ipython notebook --no-browser --ip=0.0.0.0 --port 8888
