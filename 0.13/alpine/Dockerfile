FROM alpine:3.3

# Link the musl libc library to the location where Go expects it to be.
# http://stackoverflow.com/questions/34729748/installed-go-binary-not-found-in-path-on-alpine-linux-docker
RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2

ENV TELEGRAF_VERSION 0.13.0
RUN apk add --no-cache --virtual .build-deps wget tar ca-certificates && \
    update-ca-certificates && \
    wget -q https://dl.influxdata.com/telegraf/releases/telegraf-${TELEGRAF_VERSION}_linux_amd64.tar.gz && \
    mkdir -p /usr/src && \
    tar -C /usr/src -xzf telegraf-${TELEGRAF_VERSION}_linux_amd64.tar.gz && \
    chmod +x /usr/src/*/usr/bin/* && \
    cp -a /usr/src/telegraf-*/* / && \
    rm -rf *.tar.gz /usr/src && \
    apk del .build-deps

EXPOSE 8125/udp 8092/udp 8094

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["telegraf"]
