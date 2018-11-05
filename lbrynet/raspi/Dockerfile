FROM arm32v6/python:3.7.0-alpine3.8

LABEL com.walidmujahid.name="raspi_lbrynet"
LABEL com.walidmujahid.version="0.5.0"
LABEL com.walidmujahid.author.name="Walid Mujahid وليد مجاهد"
LABEL com.walidmujahid.author.email="walid.mujahid.dev@gmail.com"
LABEL com.walidmujahid.author.keybase="walidmujahid"
LABEL com.walidmujahid.contributors=""

RUN apk add --update --no-cache coreutils bash git curl openssl-dev protobuf

RUN adduser lbryd --gecos GECOS --shell /bin/bash/ --disabled-password --home /data/

# Add virtualenv
RUN curl -LO https://files.pythonhosted.org/packages/33/bc/fa0b5347139cd9564f0d44ebd2b147ac97c36b2403943dbee8a25fd74012/virtualenv-16.0.0.tar.gz && \
    tar xvfz virtualenv-16.0.0.tar.gz && \
    cd virtualenv-16.0.0 && \
    python setup.py install

# Add lbry-sdk
RUN git clone https://github.com/lbryio/lbry.git && \
    cd lbry && \
    virtualenv lbry-venv --python=python3.7 && \
    source lbry-venv/bin/activate && \
    pip install --editable .[test]

WORKDIR lbry

# Daemon port
EXPOSE 4444
# Wallet port
EXPOSE 50001

USER lbryd
CMD ["lbrynet", "start"]
