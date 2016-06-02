FROM alpine:3.3

RUN apk add --update ca-certificates wget gnupg tar && \
    rm /var/cache/apk/*

RUN gpg --keyserver hkp://ha.pool.sks-keyservers.net \
    --recv-keys 05CE15085FC09D18E99EFB22684A14CF2582E0C5

RUN wget -q https://dl.influxdata.com/telegraf/nightlies/telegraf-static-nightly_linux_amd64.tar.gz && \
    wget -q https://dl.influxdata.com/telegraf/nightlies/telegraf-static-nightly_linux_amd64.tar.gz.asc && \
    gpg --batch --verify telegraf-static-nightly_linux_amd64.tar.gz.asc telegraf-static-nightly_linux_amd64.tar.gz && \
    tar -xvzf telegraf-static-nightly_linux_amd64.tar.gz && \
    mv -v telegraf*/* /usr/bin/ && \
    rm -f /usr/bin/telegraf.conf && \
    rm -rf telegraf-static-nightly_linux_amd64.tar.gz

EXPOSE 8125/udp 8092/udp 8094

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["/telegraf"]
