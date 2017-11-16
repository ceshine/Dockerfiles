FROM ubuntu:16.04

# MAINTAINER CeShine Lee ceshine@ceshine.net

ARG PYTHON_VERSION=3.6
ARG CONDA_PYTHON_VERSION=3
ARG CONDA_DIR=/opt/conda
ARG USERNAME=docker
ARG USERID=1000

# RUN sed -i 's/http:\/\/archive.ubuntu.com/http:\/\/mirror.internode.on.net\/pub\/ubuntu/g' /etc/apt/sources.list
# Instal basic utilities
RUN apt-get update && \
  apt-get install -y --no-install-recommends git wget unzip bzip2 sudo build-essential locales && \
  locale-gen en_US en_US.UTF-8 && \
  apt-get clean && rm -rf /var/lib/apt/lists/*

RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y
RUN DEBIAN_FRONTEND=noninteractive locale-gen en_US en_US.UTF-8

# Install miniconda
ENV PATH $CONDA_DIR/bin:$PATH
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y --no-install-recommends ca-certificates && \
  wget --quiet https://repo.continuum.io/miniconda/Miniconda$CONDA_PYTHON_VERSION-latest-Linux-x86_64.sh -O /tmp/miniconda.sh && \
  echo 'export PATH=$CONDA_DIR/bin:$PATH' > /etc/profile.d/conda.sh && \
  /bin/bash /tmp/miniconda.sh -b -p $CONDA_DIR && \
  rm -rf /tmp/* && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

# Install compile tools
RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
  apt-get install -y --no-install-recommends gfortran libatlas-base-dev libfreetype6-dev \
      cmake g++  make patch && \
  apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Python and core packages
RUN conda install -y --quiet python=$PYTHON_VERSION && \
    conda install -y --quiet h5py  numpy scipy scikit-learn pandas numba tqdm\
                             mkl-service matplotlib jupyter cython && \
    conda clean -tipsy

# Install visualization tools
RUN DEBIAN_FRONTEND=noninteractive pip install -U seaborn plotly plotnine

# Install pymc
# RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git
# RUN DEBIAN_FRONTEND=noninteractive pip install -U Theano patsy
# RUN DEBIAN_FRONTEND=noninteractive pip install git+https://github.com/pymc-devs/pymc3

# LightGBM
RUN DEBIAN_FRONTEND=noninteractive conda install -y numpy scipy scikit-learn pandas && \
    cd /usr/local/src && git clone --recursive https://github.com/Microsoft/LightGBM && \
    cd LightGBM/python-package && python setup.py install && \
    rm -rf /usr/local/src/*

# Install xgboost
RUN cd /usr/local/src && git clone --recursive https://github.com/dmlc/xgboost.git  && \
    cd xgboost && sh build.sh && cd python-package && python setup.py install && \
    rm -rf /usr/local/src

# Install catboost
RUN pip install catboost

# Setting up working directory
RUN mkdir /lab
WORKDIR /lab

# Minimize image size
RUN apt-get autoremove -y && apt-get clean -y

# Create the user
RUN useradd --create-home -s /bin/bash --no-user-group -u $USERID $USERNAME && \
    chown -R $USERNAME $CONDA_DIR
RUN adduser $USERNAME sudo && \
    echo "$USERNAME ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
USER $USERNAME

# Setting up jupyter notebook server
EXPOSE 8888
RUN jupyter nbextension enable --py widgetsnbextension
CMD jupyter notebook --no-browser --ip=0.0.0.0 --port 8888
