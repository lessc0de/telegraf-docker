FROM buildpack-deps:trusty-curl

RUN gpg \
    --keyserver hkp://ha.pool.sks-keyservers.net \
    --recv-keys 05CE15085FC09D18E99EFB22684A14CF2582E0C5

RUN wget -q https://dl.influxdata.com/telegraf/nightlies/telegraf_nightly_amd64.deb.asc && \
    wget -q https://dl.influxdata.com/telegraf/nightlies/telegraf_nightly_amd64.deb && \
    gpg --batch --verify https://dl.influxdata.com/telegraf/nightlies/telegraf_nightly_amd64.deb.asc \
                         https://dl.influxdata.com/telegraf/nightlies/telegraf_nightly_amd64.deb && \
    dpkg -i telegraf_nightly_amd64.deb && \
    rm -f telegraf_nightly_amd64.deb*

EXPOSE 8125/udp 8092/udp 8094

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["telegraf"]
