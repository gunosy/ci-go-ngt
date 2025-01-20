FROM gunosy/ci-go:1.13

ENV NGT_VERSION=1.12.1

RUN apt --allow-releaseinfo-change update \
  && apt install -y --no-install-recommends cmake \
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
