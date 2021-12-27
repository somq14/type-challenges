FROM debian:11.2
SHELL ["/bin/bash", "-c"]

ARG NODE_VERSION=16.13.1
ARG YARN_VERSION=1.22.17
ARG PYTHON_VERSION=3.10.1

RUN apt update \
    && apt install -y \
        vim \
        git \
        curl \
        zip \
    && apt clean \
    && rm -rf /var/lib/apt/lists/*

# install node.js with fnm
RUN curl -fsSL https://fnm.vercel.app/install | bash \
    && source ~/.bashrc \
    && fnm install ${NODE_VERSION} \
    && fnm use ${NODE_VERSION} \
    && npm install -g yarn@${YARN_VERSION}

# install python build requirements
RUN apt update \
    && apt install -y \
        locales \
        make \
        build-essential \
        libssl-dev \
        zlib1g-dev \
        libbz2-dev \
        libreadline-dev \
        libsqlite3-dev \
        wget \
        curl \
        llvm \
        libncursesw5-dev \
        xz-utils \
        tk-dev \
        libxml2-dev \
        libxmlsec1-dev \
        libffi-dev \
        liblzma-dev \
    && apt clean \
    && rm -rf /var/lib/apt/lists/* \
    # en_US.UTF-8 を有効にする (https://hub.docker.com/_/debian)
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

# install pyenv
RUN curl https://pyenv.run | bash \
    && echo '' >> ~/.bashrc \
    && echo '# pyenv' >> ~/.bashrc \
    && echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc \
    && echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc \
    && echo 'eval "$(pyenv init --path)"' >> ~/.bashrc \
    && echo 'eval "$(pyenv init -)"' >> ~/.bashrc

# install python
RUN source ~/.bashrc \
    && pyenv install ${PYTHON_VERSION} \
    && pyenv global ${PYTHON_VERSION}
