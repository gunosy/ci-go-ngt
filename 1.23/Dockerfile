FROM golang:1.23

ENV NGT_VERSION=1.12.1
ENV GOLANGCI_LINT_VERSION=v1.62.2

RUN apt --allow-releaseinfo-change update \
  && apt install -y --no-install-recommends cmake make libssl-dev libghc-zlib-dev libcurl4-gnutls-dev libexpat1-dev gettext unzip git \
  && apt clean \
  && rm -rf /var/lib/apt/lists/* \
  && mkdir -p /ngt \
  && wget -P /ngt https://github.com/yahoojapan/NGT/archive/v${NGT_VERSION}.tar.gz \
  && tar xvf /ngt/v${NGT_VERSION}.tar.gz -C /ngt \
  && mkdir /ngt/NGT-${NGT_VERSION}/build \
  && cd /ngt/NGT-${NGT_VERSION}/build \
  && cmake .. \
  && make \
  && make install \
  && ldconfig \
  && cd /go \
  && rm -rf /ngt

RUN GO111MODULE=on go get github.com/golangci/golangci-lint/cmd/golangci-lint@${GOLANGCI_LINT_VERSION}
