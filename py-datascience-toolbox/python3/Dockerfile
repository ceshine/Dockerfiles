FROM ubuntu:14.04

# MAINTAINER CeShine Lee ceshine@ceshine.net

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y
RUN DEBIAN_FRONTEND=noninteractive locale-gen en_US en_US.UTF-8

# Install python packages
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y python3 python3-pip ipython3 \ 
    ipython3-notebook python3-numpy python3-scipy python3-matplotlib python3-pandas
RUN DEBIAN_FRONTEND=noninteractive pip3 install -U scikit-learn

# Install git
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git-core

# Need to update ipython or ipython notebook will crash
RUN DEBIAN_FRONTEND=noninteractive pip3 install ipython --upgrade

#Setting up working directory
RUN mkdir /lab 
WORKDIR /lab

#Minimize image size
RUN (apt-get autoremove -y; \
     apt-get clean -y)

#Setting up ipython notebook server
EXPOSE 8888
CMD ipython notebook --no-browser --ip=0.0.0.0 --port 8888
