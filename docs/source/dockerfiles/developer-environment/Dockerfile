ARG BASE_CONTAINER=jupyter/tensorflow-notebook
FROM $BASE_CONTAINER

LABEL maintainer="researchdevresources <psam012@aucklanduni.ac.nz>"
ARG NB_USER="jovyan"
ARG NB_UID="1000"
ARG NB_GID="100"

# Fix DL4006
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

# Install all OS dependencies for notebook server that starts but lacks all
# features (e.g., download as all possible file formats)
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
 && apt-get install -yq --no-install-recommends \
    wget \
    bzip2 \
    ca-certificates \
    sudo \
    locales \
    fonts-liberation \
    run-one \
    git \
    make \
    cmake \
    libssl-dev \
    sudo \
    cifs-utils \
    systemd \
    openssh-server \
    software-properties-common \
 && apt-get clean && rm -rf /var/lib/apt/lists/*

#----------------------------
# Install cmake.
ENV CMAKE_VERSION=3.16.3 \
    CMAKE_DIR=/cmake

RUN wget --quiet https://cmake.org/files/v3.16/cmake-${CMAKE_VERSION}-Linux-x86_64.sh && \
    mkdir $CMAKE_DIR && \
    /bin/bash cmake-${CMAKE_VERSION}-Linux-x86_64.sh --skip-license --prefix=$CMAKE_DIR && \
    rm cmake-${CMAKE_VERSION}-Linux-x86_64.sh
ENV PATH=$CMAKE_DIR/bin:$PATH

# Install ssh server.
RUN mkdir /var/run/sshd
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

USER $NB_UID

ENV JUPYTER_ALLOW_INSECURE_WRITES=true

ENV PATH="/home/${NB_USER}/.local/bin":$PATH

USER root

# Pycharm dependencies
RUN apt-get update && apt-get install --no-install-recommends -y \
  less libgbm-dev \
  libxtst-dev libxext-dev libxrender-dev libfreetype6-dev \
  libfontconfig1 libgtk2.0-0 libxslt1.1 libxxf86vm1 \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

# Visual studio code dependencies 
RUN apt-get update && apt-get install --no-install-recommends -y \
  libc6-dev libgtk2.0-0 libgtk-3-0 libpango-1.0-0 libcairo2 \
  libfontconfig1 libnss3 libasound2 libxtst6 unzip \
  libglib2.0-bin libcanberra-gtk-module libgl1-mesa-glx curl \
  build-essential gettext libstdc++6 software-properties-common \
  wget git xterm automake libtool autogen nodejs libnotify-bin \
  aspell aspell-en htop git mono-complete gvfs-bin libxss1 \
  rxvt-unicode-256color x11-xserver-utils sudo vim libxkbfile1 libnss3 \
  && sudo apt-get install -f --no-install-recommends -y \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

#----------------------------

USER $NB_UID

RUN pip install \
    'sphinx' \
    'sphinx-rtd-theme' \
    'sphinxcontrib-bibtex'

WORKDIR $HOME

# Expose multiple ports (Jupyter notebook and ssh).
EXPOSE 8888 22


