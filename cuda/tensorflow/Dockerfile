FROM tensorflow/tensorflow:1.8.0-gpu-py3

MAINTAINER CeShine Lee <ceshine@ceshine.net>

# Based on https://github.com/anurag/fastai-course-1/
ARG USERNAME=docker
ARG USERID=1000

ENV LANG C.UTF-8

# Instal basic utilities
RUN apt-get update && \
  apt-get install -y --no-install-recommends git wget unzip bzip2 sudo build-essential libjpeg-dev && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

# Create the user
RUN useradd --create-home -s /bin/bash --no-user-group -u $USERID $USERNAME && \
    adduser $USERNAME sudo && \
    echo "$USERNAME ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN  pip install --upgrade pip && \
  pip install -U jupyter h5py pandas==0.22.0 sklearn matplotlib seaborn plotly pillow-simd joblib tqdm

USER $USERNAME
WORKDIR /home/$USERNAME

# Jupyter
EXPOSE 8888
CMD jupyter notebook --ip=0.0.0.0 --port=8888
