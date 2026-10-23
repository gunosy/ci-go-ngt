FROM gunosy/ci-go:1.13 AS go-toolchain

FROM debian:bookworm-slim
COPY --from=go-toolchain /usr/local/go /usr/local/go
COPY --from=go-toolchain /go/bin/golangci-lint /go/bin/golangci-lint

ENV GOPATH=/go
ENV PATH=/go/bin:/usr/local/go/bin:$PATH
ENV GOLANG_VERSION=1.13.15
ENV GOLANGCI_LINT_VERSION=v1.25.1
ENV NGT_VERSION=1.12.1

RUN apt-get update \
  && apt-get install -y --no-install-recommends build-essential ca-certificates cmake curl git wget \
  && update-ca-certificates --fresh \
  && dpkg --compare-versions "$(dpkg-query -W -f='${Version}' ca-certificates)" ge '20250419~deb12u2' \
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
