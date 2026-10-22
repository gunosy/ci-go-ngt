FROM golang:1.23 AS go-toolchain

FROM debian:bookworm-slim
COPY --from=go-toolchain /usr/local/go /usr/local/go

ENV GOPATH=/go
ENV PATH=/go/bin:/usr/local/go/bin:$PATH
ENV GOLANG_VERSION=1.23.12
ENV GOTOOLCHAIN=local
ENV NGT_VERSION=1.12.1
ENV GOLANGCI_LINT_VERSION=v1.62.2

RUN apt-get update \
  && apt-get install -y --no-install-recommends build-essential ca-certificates cmake gettext git libcurl4-gnutls-dev libexpat1-dev libghc-zlib-dev libssl-dev unzip wget \
  && update-ca-certificates --fresh \
  && rm -rf /var/lib/apt/lists/* \
  && mkdir -p /go /ngt \
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

RUN GO111MODULE=on go install github.com/golangci/golangci-lint/cmd/golangci-lint@${GOLANGCI_LINT_VERSION}
