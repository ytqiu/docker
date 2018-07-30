FROM ubuntu:xenial

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

EXPOSE 5000

RUN useradd --create-home redash

# Ubuntu packages
RUN apt-get update && apt-get install -y curl apt-transport-https
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update
RUN apt-get install -y python-pip python-dev build-essential pwgen libffi-dev sudo git-core wget \
  #nodejs \
  yarn \
  # Postgres client
  libpq-dev \
  # for SAML
  xmlsec1 \
  # Additional packages required for data sources:
  libssl-dev libmysqlclient-dev freetds-dev libsasl2-dev && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

RUN wget https://nodejs.org/dist/v8.11.3/node-v8.11.3-linux-x64.tar.xz
RUN tar vxf node-v8.11.3-linux-x64.tar.xz && mv node-v8.11.3-linux-x64/bin/* /usr/bin && rm -rf node-v8.11.3-linux-x64*

RUN pip install -i https://pypi.doubanio.com/simple/ --upgrade pip
RUN pip install -i https://pypi.doubanio.com/simple/ -U setuptools==23.1.0

WORKDIR /app
