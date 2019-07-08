## -*- docker-image-name: "fayoh/stm8-dev" -*-
LABEL maintainer="daniel.f.bengtsson@gmail.com"
LABEL Description="Dev image for stm8 micros"

ARG http_proxy
ARG https_proxy

FROM ubuntu:rolling as builder
RUN     apt-get update && apt-get install -y \
        gcc git libusb-1.0-0 libusb-1.0-0-dev make pkg-config && \
        git clone --depth=1 https://github.com/vdudouyt/stm8flash.git && \
        cd stm8flash && make && make install && \
        cd - && rm -rf stm8flash && \
        git clone --depth=1 https://github.com/fayoh/stm8s-util.git && \
        cd stm8s-util && \
        make install && cd - && \
        rm -rf stm8s-util

FROM ubuntu:rolling
RUN     apt-get update && apt-get install -y wget make libusb-1.0-0 && \
        rm -rf /var/lib/apt/lists && \
        wget -q https://datapacket.dl.sourceforge.net/project/sdcc/sdcc-linux-amd64/3.9.0/sdcc-3.9.0-amd64-unknown-linux2.5.tar.bz2 -O sdcc.tar.bz2 && \
        tar xjf sdcc.tar.bz2 && \
        cp -r sdcc-3.9.0/* /usr/local && \
        rm -rf sdcc-3.9.0 sdcc.tar.bz2
COPY    --from=builder /usr/local/bin/stm8flash /usr/local/bin/stm8flash
COPY    --from=builder /usr/share/sdcc/include/stm8s.h /usr/local/share/sdcc/include/
ENV     http_proxy=$http_proxy https_proxy=$https_proxy

