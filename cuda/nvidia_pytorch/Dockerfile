# An example Dockerfile that add more deep learining libraries to nvidia/pytorch
FROM nvcr.io/nvidia/pytorch:22.01-py3

# Install rclone
RUN wget https://downloads.rclone.org/v1.58.1/rclone-v1.58.1-linux-amd64.zip && \
    unzip rclone-v1.58.1-linux-amd64.zip && \
    mv rclone-v1.58.1-linux-amd64/rclone /usr/bin/ && \
    rm rclone-v1.58.1-linux-amd64.zip && \
    rm -rf rclone-v1.58.1-linux-amd64

# Install mamba
RUN conda install -c conda-forge mamba && conda clean -ay

# Install PyTorch Lightining and other ML libraries
RUN pip install --no-cache pytorch-lightning==1.5.10 \
    torchmetrics==0.7.3 https://github.com/veritable-tech/pytorch-lightning-spells/archive/pl_1_5.zip \
    https://github.com/rwightman/pytorch-image-models/archive/master.zip \
    wandb watermark python-dotenv albumentations==1.0.3 tensorflow-cpu tensorflow-datasets \
    fastcore==1.3.20 typer omegaconf


# Create a user
ARG USERNAME=docker
ARG USERID=1000
RUN useradd --create-home -d /users/$USERNAME -s /bin/bash --no-user-group -u $USERID $USERNAME && \
    adduser $USERNAME sudo && \
    echo "$USERNAME ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers