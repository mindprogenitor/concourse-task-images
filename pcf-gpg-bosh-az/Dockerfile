FROM alpine:edge

WORKDIR /root

RUN apk --no-cache add bash curl jq ruby gnupg

RUN curl -skL "$(curl -s https://api.github.com/repos/pivotal-cf/om/releases/latest|jq --raw-output '.assets[] | .browser_download_url' | grep linux | grep -v zip)" > /usr/bin/om-linux && chmod 755 /usr/bin/om-linux

RUN curl -skL "$(curl -s https://api.github.com/repos/pivotal-cf/pivnet-cli/releases/latest|jq --raw-output '.assets[] | .browser_download_url' | grep linux | grep -v zip)" > /usr/bin/pivnet-cli && chmod 755 /usr/bin/pivnet-cli

RUN curl -skL https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-2.0.48-linux-amd64 > /usr/local/bin/bosh2 && chmod 0755 /usr/local/bin/bosh2

RUN apk --no-cache add \
  ruby-dev \
  make \
  gcc \
  libc-dev ; \
  gem install json -N ; \
  gem install bosh_cli -N ; \
  apk del \
  libc-dev \
  gcc \
  make \
  ruby-dev ; \
  rm -fr /tmp/* ; \
  rm -fr /var/cache/apk

COPY install_input /tmp/install_input

RUN apk --no-cache add \
  tar \
  openssl \
  python \
  gcc \
  libffi \
  libffi-dev \
  libc-dev \ 
  python-dev \
  openssl-dev \
  make ; \
  curl -L https://aka.ms/InstallAzureCli | sed s/XXXX/XXXXXX/ | sed s/_TTY=\\/dev\\/tty// | sed s/'< $_TTY'// > /tmp/install_azure_cli.sh ; \
  bash /tmp/install_azure_cli.sh < /tmp/install_input ; \
  apk del \
  openssl-dev \
  libffi-dev \
  python-dev \
  libc-dev \
  gcc \
  make \
  tar ; \
  rm -fr /tmp/* ; \
  rm -fr /var/cache/apk

