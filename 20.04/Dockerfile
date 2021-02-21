FROM ubuntu:20.04

ARG PULSAR_VERSION=2.5.2
ARG PULSAR_URL_PREFIX=https://archive.apache.org/dist/pulsar/pulsar-${PULSAR_VERSION}
ARG PULSAR_CLIENT=apache-pulsar-client.deb
RUN set -x \
    && sed -i 's/archive.ubuntu.com/mirrors.huaweicloud.com/g' /etc/apt/sources.list \
    ## install by apt-get
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    libboost-dev libboost-filesystem-dev \
    liblz4-dev libsnappy-dev libzstd-dev liblog4cxx-dev \
    libmsgpack-dev libzookeeper-mt-dev libcpprest-dev libhdf5-dev \
    netcat-openbsd \
    python3-h5py python3-numpy python3-scipy python3-matplotlib python3-tk \
    wget \
    ## install pulsar c++ client
    && mkdir -pv /tmp/pulsar/DEB \
    && cd /tmp/pulsar \
    && wget -q "${PULSAR_URL_PREFIX}/DEB/${PULSAR_CLIENT}" -P "DEB" \
    && wget -q "${PULSAR_URL_PREFIX}/DEB/${PULSAR_CLIENT}.sha512" -P "DEB" \
    && sha512sum -c "DEB/${PULSAR_CLIENT}.sha512" \
    && dpkg -i "DEB/${PULSAR_CLIENT}" \
    && cd / \
    && rm -rf /tmp/pulsar \
    ## clean
    && apt-get autoremove -y wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

CMD ["/bin/bash"]
