FROM nvidia/cuda:8.0-cudnn7-devel-ubuntu16.04

MAINTAINER CeShine Lee <ceshine@ceshine.net>

# Based on https://github.com/anurag/fastai-course-1/

ARG PYTHON_VERSION=3.6
ARG CONDA_PYTHON_VERSION=3
ARG CONDA_DIR=/opt/conda
ARG USERNAME=docker
ARG USERID=1000

# Instal basic utilities
RUN apt-get update && \
  apt-get install -y --no-install-recommends git wget unzip bzip2 \
        sudo build-essential libjpeg-dev libpng-dev libnccl2=2.0.5-2+cuda8.0 \
        libnccl-dev=2.0.5-2+cuda8.0 && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

# Install miniconda
ENV PATH $CONDA_DIR/bin:$PATH
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates && \
  wget --quiet https://repo.continuum.io/miniconda/Miniconda$CONDA_PYTHON_VERSION-latest-Linux-x86_64.sh -O /tmp/miniconda.sh && \
  echo 'export PATH=$CONDA_DIR/bin:$PATH' > /etc/profile.d/conda.sh && \
  /bin/bash /tmp/miniconda.sh -b -p $CONDA_DIR && \
  rm -rf /tmp/* && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

# Create the user
RUN useradd --create-home -s /bin/bash --no-user-group -u $USERID $USERNAME && \
    chown $USERNAME $CONDA_DIR -R && \
    adduser $USERNAME sudo && \
    echo "$USERNAME ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER $USERNAME
WORKDIR /home/$USERNAME

ENV CMAKE_PREFIX_PATH $CONDA_DIR
ENV TORCH_CUDA_ARCH_LIST "3.5 5.2 6.0 6.1+PTX"
ENV TORCH_NVCC_FLAGS "-Xfatbin -compress-all"

RUN conda install -y --quiet python=$PYTHON_VERSION && \
  conda install -y --quiet h5py scikit-learn \
  pandas mkl-service pyyaml mkl cmake cffi setuptools && \
  conda install -y magma-cuda80 -c soumith && \
  conda clean -tipsy

RUN git clone --recursive https://github.com/pytorch/pytorch.git && cd pytorch && \
    python setup.py install && cd .. && rm -rf pytorch
RUN git clone https://github.com/pytorch/vision.git && cd vision && pip install -v .

RUN  pip install --upgrade pip && \
  pip install pillow-simd

ENV CUDA_HOME=/usr/local/cuda
ENV CUDA_ROOT=$CUDA_HOME
ENV PATH=$PATH:$CUDA_ROOT/bin:$HOME/bin
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CUDA_ROOT/lib64
