FROM rancher/agent-base:v0.3.0
ENV CNI v0.3.0
ENV RANCHER_CNI_BRIDGE v0.3.1
ENV RANCHER_CNI_IPAM v0.1.1

# https://github.com/rancher/rancher-cni-ipam/
COPY ./rancher-cni-ipam-0.1.1.tar.gz /

# https://github.com/rancher/rancher-cni-bridge/
COPY ./rancher-cni-bridge-v0.3.1.tar.gz /

# https://github.com/rancher/strongswan-package
ADD strongswan.tar.gz /

RUN mkdir -p /opt/cni/bin /etc/cni/net.d  /usr/local/etc/strongswan.d \
    && echo 'charon {\n\tmake_before_break = yes\n}' > /usr/local/etc/strongswan.d/charon.conf \
    # aarch64
    && curl -sfSL https://github.com/containernetworking/cni/releases/download/v0.4.0/cni-arm64-v0.4.0.tgz | tar xvzf - -C /tmp ./loopback \
    && tar xvzf /rancher-cni-ipam-0.1.1.tar.gz -C /tmp \
    && tar xvzf /rancher-cni-bridge-v0.3.1.tar.gz -C /tmp \
    && mv /tmp/rancher-cni-bridge /tmp/rancher-bridge \
    && mv /tmp/* /opt/cni/bin

COPY start.sh start-vxlan.sh rancher-net /usr/bin/
CMD ["start.sh"]
