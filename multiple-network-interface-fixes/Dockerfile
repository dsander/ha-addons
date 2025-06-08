ARG BUILD_FROM
FROM $BUILD_FROM


RUN \
    set -x && \
    apk add --no-cache \
        networkmanager-cli

COPY rootfs /

RUN \
    set -x && \
    chmod a+x /usr/bin/mnifix*  &&\
    chmod a+x /etc/s6-overlay/scripts/* &&\
    chmod a+x /etc/s6-overlay/s6-rc.d/mnifix/*
