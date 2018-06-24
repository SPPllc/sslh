FROM debian:stretch as bldr

ARG SSLH_VERSION=v1.19c

RUN set -x \
  && apt-get update \
  && apt-get install -y --no-install-recommends \
    build-essential ca-certificates git \
    libpcre3-dev libwrap0-dev libconfig8-dev
RUN git clone https://github.com/mwlczk/sslh.git \
    --branch $SSLH_VERSION \
    --single-branch --depth=1
RUN cd sslh \
  && make install \
  && make


FROM debian:stretch-slim

ARG SSLH_UID=999
ARG SSLH_GID=999

COPY --from=bldr /sslh/sslh-fork /usr/local/sbin/sslh
COPY --from=bldr /sslh/basic.cfg /etc/sslh.cfg

# RUN set -x \
#   && cp sslh-fork /usr/local/sbin/sslh \
#   && cp basic.cfg /etc/sslh.cfg
