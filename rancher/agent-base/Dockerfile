FROM aarch64/ubuntu:16.04 

COPY ./rancher-entrypoint.sh /

# https://github.com/rancher/runc/tree/share-mnt-v0.2.1
COPY ./share-mnt /usr/bin/

# https://github.com/rancher/weave/tree/r-v0.0.4/prog/weavewait
COPY ./r /usr/bin/

ENV SSL_SCRIPT_COMMIT 98660ada3d800f653fc1f105771b5173f9d1a019

RUN apt-get update && \
        apt-get install --no-install-recommends -y \
        arptables \
        bridge-utils \
        ca-certificates \
        conntrack \
        curl \
        ethtool \
        iproute2 \
        iptables \
        iputils-ping \
        jq \
        kmod \
        openssl \
        psmisc \
        python2.7 \
        tcpdump \
        vim-tiny && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir -p /var/lib/cattle /var/lib/rancher && \
    ln -s /usr/bin/python2.7 /usr/bin/python && \
    curl -s https://bootstrap.pypa.io/get-pip.py | python2.7 && \
    pip install cattle && \
    # aarch64
    curl -sLf https://github.com/rancher/docker/releases/download/v1.10.3-ros1/docker-1.10.3_arm64 > /usr/bin/docker && \
    chmod +x /usr/bin/docker && \
    rm /var/run && \
    mkdir /var/run && \
    curl -sLf https://raw.githubusercontent.com/rancher/rancher/${SSL_SCRIPT_COMMIT}/server/bin/update-rancher-ssl > /usr/bin/update-rancher-ssl && \
    chmod +x /usr/bin/update-rancher-ssl

ENTRYPOINT ["/rancher-entrypoint.sh"]
