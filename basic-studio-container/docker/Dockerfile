FROM python:3.8

# As of 2021-11-03, SageMaker only supports 1000/100 or 0/0 as the possible UID/GID values.
ARG NB_USER="sagemaker-user"
ARG NB_UID="1000"
ARG NB_GID="100"

# Setup the "sagemaker-user" user with root privileges.
RUN \
    apt-get update && \
    apt-get install -y sudo && \
    useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && \
    chmod g+w /etc/passwd && \
    echo "${NB_USER}    ALL=(ALL)    NOPASSWD:    ALL" >> /etc/sudoers && \
    # Prevent apt-get cache from being persisted to this layer.
    rm -rf /var/lib/apt/lists/*
    
# Make the default shell bash (vs "sh") for a better Jupyter terminal UX
ENV SHELL=/bin/bash
ENV PATH="/home/sagemaker-user/.local/bin:${PATH}"

RUN pip install ipykernel && \
        python -m ipykernel install --sys-prefix

USER $NB_UID


