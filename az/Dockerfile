FROM alpine:edge

RUN apk --no-cache add \
  bash \
  curl \
  jq \
  tar \
  openssl \
  python \
  gcc \
  libffi \
  libffi-dev \
  libc-dev \ 
  python-dev \
  openssl-dev \
  make

WORKDIR /root

COPY install_input /tmp/install_input
RUN curl -L https://aka.ms/InstallAzureCli | sed s/XXXX/XXXXXX/ | sed s/_TTY=\\/dev\\/tty// | sed s/'< $_TTY'// > /tmp/install_azure_cli.sh
RUN bash /tmp/install_azure_cli.sh < /tmp/install_input

RUN apk del \
  openssl-dev \
  libffi-dev \
  python-dev \
  libc-dev \
  gcc \
  make \
  tar \
  apk-tools

RUN rm -fr /tmp/*
