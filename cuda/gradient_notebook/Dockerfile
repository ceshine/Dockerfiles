# FROM ubuntu:22.04 AS build
# FROM nvidia/cuda:11.7.0-devel-ubuntu20.04 AS build
FROM nvidia/cuda:11.8.0-base-ubuntu22.04 AS build

LABEL maintainer="Ceshine Lee <ceshine@ceshine.net>"

ARG PYTHON_VERSION=3.10
ARG CONDA_PYTHON_VERSION=3
ARG CONDA_DIR=/opt/conda
# ARG USERNAME=docker
# ARG USERID=1000

# Install basic utilities
RUN  apt-get update \
    && apt-get install --no-install-recommends -yy gnupg git wget unzip bzip2 sudo build-essential byobu \
    && apt-get clean all \
    && rm /var/log/apt/* /var/log/alternatives.log /var/log/bootstrap.log /var/log/dpkg.log

# # Create the user
# RUN useradd --create-home -d /users/$USERNAME -s /bin/bash --no-user-group -u $USERID $USERNAME && \
#     adduser $USERNAME sudo && \
#     echo "$USERNAME ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Install mamba
ENV PATH $CONDA_DIR/bin:$PATH
COPY environment.yml .
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates && \
    # wget -q https://repo.continuum.io/miniconda/Miniconda$CONDA_PYTHON_VERSION-latest-Linux-x86_64.sh -O /tmp/miniconda.sh && \
    wget -q  https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh -O /tmp/mambaforge.sh && \
    echo 'export PATH=$CONDA_DIR/bin:$PATH' > /etc/profile.d/conda.sh && \
    /bin/bash /tmp/mambaforge.sh -b -p $CONDA_DIR && \
    # chown $USERNAME $CONDA_DIR -R && \
    mamba env update --name base --file ./environment.yml && \
    conda clean -ay && \
    rm -rf /tmp/* && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install rclone
RUN wget https://downloads.rclone.org/v1.58.1/rclone-v1.58.1-linux-amd64.zip && \
    unzip rclone-v1.58.1-linux-amd64.zip && \
    mv rclone-v1.58.1-linux-amd64/rclone /usr/bin/ && \
    rm rclone-v1.58.1-linux-amd64.zip && \
    rm -rf rclone-v1.58.1-linux-amd64

# xformers built in this way does not work on CUDA...
# ENV TORCH_CUDA_ARCH_LIST="7.5 8.6"
# RUN TORCH_CUDA_ARCH_LIST="7.5;8.6" pip install --no-cache git+https://github.com/facebookresearch/xformers.git@0bad001ddd56c080524d37c84ff58d9cd030ebfd#egg=xformers

CMD ["jupyter", "lab", "--allow-root", "--ip=0.0.0.0", "--no-browser", "--ServerApp.trust_xheaders=True", "--ServerApp.disable_check_xsrf=False", "--ServerApp.allow_remote_access=True", "--ServerApp.allow_origin='*'", "--ServerApp.allow_credentials=True"]

# jupyter lab --allow-root --ip=0.0.0.0 --no-browser --ServerApp.trust_xheaders=True --ServerApp.disable_check_xsrf=False --ServerApp.allow_remote_access=True --ServerApp.allow_origin='*' --ServerApp.allow_credentials=True

# Runtime image
# FROM ubuntu:20.04
# FROM nvidia/cuda:11.7.0-base-ubuntu20.04

# ARG CONDA_DIR=/opt/conda
# ARG USERNAME=docker
# ARG USERID=1000
# ENV PATH $CONDA_DIR/bin:$PATH
# ENV PATH=$PATH:$HOME/bin

# # Install basic utilities
# RUN  apt-get update \
#     && apt-get install --no-install-recommends -yy gnupg git wget unzip bzip2 sudo build-essential byobu ca-certificates \
#     && apt-get clean all \
#     && rm /var/log/apt/* /var/log/alternatives.log /var/log/bootstrap.log /var/log/dpkg.log

# RUN mkdir -p /opt/conda/
# # Install rclone
# RUN wget https://downloads.rclone.org/v1.58.1/rclone-v1.58.1-linux-amd64.zip && \
#     unzip rclone-v1.58.1-linux-amd64.zip && \
#     mv rclone-v1.58.1-linux-amd64/rclone /usr/bin/ && \
#     rm rclone-v1.58.1-linux-amd64.zip && \
#     rm -rf rclone-v1.58.1-linux-amd64

# # Create the user
# RUN useradd --create-home -s /bin/bash --no-user-group -u $USERID $USERNAME && \
#     chown $USERNAME $CONDA_DIR -R && \
#     adduser $USERNAME sudo && \
#     echo "$USERNAME ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
# USER $USERNAME
# WORKDIR /src

# COPY --chown=1000 --from=build /opt/conda/. $CONDA_DIR

# USER $USERNAME
# WORKDIR /users/$USERNAME

# CMD ["jupyter", "lab", "--allow-root", "--ip=0.0.0.0", "--no-browser", "--ServerApp.trust_xheaders=True", "--ServerApp.disable_check_xsrf=False", "--ServerApp.allow_remote_access=True", "--ServerApp.allow_origin='*'", "--ServerApp.allow_credentials=True"]
