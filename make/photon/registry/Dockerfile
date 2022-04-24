ARG harbor_base_image_version
FROM feiteng.harbor.ctyun.cn:5000/feitengky10/caas/photon:3.0
RUN rm -rf /etc/yum.repos.d/*
COPY ./make/photon/packages/config/harbor.repo /etc/yum.repos.d/harbor.repo

RUN tdnf install sudo -y >> /dev/null\
    && tdnf clean all \
    && mkdir -p /etc/registry \
    && groupadd -r -g 10000 harbor && useradd --no-log-init -m -g 10000 -u 10000 harbor
COPY ./make/photon/common/install_cert.sh /home/harbor
COPY ./make/photon/registry/entrypoint.sh /home/harbor
COPY ./make/photon/registry/binary/registry /usr/bin

RUN chown -R harbor:harbor /etc/pki/tls/certs \
    && chown harbor:harbor /etc/registry \
    && chown harbor:harbor /home/harbor/entrypoint.sh && chmod u+x /home/harbor/entrypoint.sh \
    && chown harbor:harbor /home/harbor/install_cert.sh && chmod u+x /home/harbor/install_cert.sh \
    && chown harbor:harbor /usr/bin/registry && chmod u+x /usr/bin/registry

ENV PGPATH /var/lib/postgresql && mkdir -p "$PGDATA" && chown -R postgres:postgres "$PGPATH" && chmod 777 "$PGPATH"

HEALTHCHECK CMD curl 127.0.0.1:5000/

USER harbor

ENTRYPOINT ["/home/harbor/entrypoint.sh"]

VOLUME ["/var/lib/registry"]
EXPOSE 5000
