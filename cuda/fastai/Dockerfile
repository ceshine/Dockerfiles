FROM nvidia/cuda:8.0-cudnn5-runtime-ubuntu16.04

MAINTAINER CeShine Lee <ceshine@ceshine.net>

# Based on https://github.com/anurag/fastai-course-1/

ARG PYTHON_VERSION=3.6
ARG CONDA_PYTHON_VERSION=3
ARG CONDA_DIR=/opt/conda
ARG USERNAME=fastai
ARG USERID=1000

# Instal basic utilities
RUN apt-get update && \
  apt-get install -y --no-install-recommends git wget ffmpeg unzip bzip2 sudo build-essential && \
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

COPY jupyter_notebook_config.py .jupyter/

RUN conda install -y --quiet python=$PYTHON_VERSION && \
  conda install -y --quiet jupyter h5py ipywidgets scikit-learn \
  matplotlib pandas bcolz sympy scikit-image mkl-service && \
  conda install pytorch=0.1.12 torchvision cuda80 -c soumith && \
  conda clean -tipsy

RUN  pip install --upgrade pip && \
  pip install tensorflow-gpu==0.12.1 kaggle-cli pillow-simd xgboost && \
  pip install git+git://github.com/fchollet/keras.git@1.1.2 && \
  pip install nltk gensim keras-tqdm

# A hack to fix an issue in older versions of tensorflow
# RUN sudo ln -s /usr/lib/x86_64-linux-gnu/libcudnn.so.5.1.10 /usr/local/cuda/lib64/libcudnn.so


ENV CUDA_HOME=/usr/local/cuda
ENV CUDA_ROOT=$CUDA_HOME
ENV PATH=$PATH:$CUDA_ROOT/bin:$HOME/bin
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CUDA_ROOT/lib64

# Jupyter
EXPOSE 8888

# Clone fast.ai source
RUN git clone -q https://github.com/fastai/courses.git fastai-courses
WORKDIR /home/$USERNAME/fastai-courses/

CMD jupyter notebook --ip=0.0.0.0 --port=8888
