FROM alpine:edge

WORKDIR /root

RUN apk --no-cache add bash curl jq ruby

RUN curl -skL "$(curl -s https://api.github.com/repos/pivotal-cf/om/releases/latest|jq --raw-output '.assets[] | .browser_download_url' | grep linux | grep -v zip)" > /usr/bin/om-linux && chmod 755 /usr/bin/om-linux

RUN curl -skL "$(curl -s https://api.github.com/repos/pivotal-cf/pivnet-cli/releases/latest|jq --raw-output '.assets[] | .browser_download_url' | grep linux | grep -v zip)" > /usr/bin/pivnet-cli && chmod 755 /usr/bin/pivnet-cli

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
  ruby-dev \
  apk-tools ; \
  rm -fr /tmp/* ; \
  rm -fr /var/cache/apk


