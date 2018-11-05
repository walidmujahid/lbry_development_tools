FROM ubuntu:18.04

# bad practice?
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y build-essential \
                       software-properties-common \
                       checkinstall \
                       libreadline-gplv2-dev \
                       libncursesw5-dev \
                       libssl-dev \
                       libsqlite3-dev \
                       tk-dev \
                       libgdbm-dev \
                       libc6-dev \
                       libbz2-dev \
                       zlib1g-dev \
                       openssl \
                       libffi-dev \
                       python3-dev \
                       python3-setuptools \
                       wget \
                       git \
                       python-virtualenv \
                       libssl-dev \
                       python-protobuf && \
    mkdir /tmp/Python37 && cd /tmp/Python37 && \
    wget https://www.python.org/ftp/python/3.7.0/Python-3.7.0.tar.xz && \
    tar xvf Python-3.7.0.tar.xz && \
    cd /tmp/Python37/Python-3.7.0 && \
    ./configure && make altinstall && \
    mkdir /lbry

WORKDIR /lbry

ENTRYPOINT ["/bin/bash"]
CMD ["-c", "virtualenv lbry-venv --python=python3.7 && \
            source lbry-venv/bin/activate && \
            pip install --editable .[test] && \
            trial --reactor=asyncio tests.unit"]
