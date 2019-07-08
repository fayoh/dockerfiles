#FROM frolvand/alpine-glibc
FROM python:3.7-slim
LABEL Description="Smallish image with devtools for esp{8266,32}"
LABEL Maintainer="daniel.f.bengtsson@gmail.com"

ARG http_proxy
ARG https_proxy


ENV ARDUINO_DIR /usr/local/src/arduino
ENV PATH /usr/local/bin:${ARDUINO_DIR}:$PATH
ENV LANG C.UTF-8
ENV ARDUINO_VER 1.8.9-linux64
ENV PYLINK "https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}tar.xz"
ENV http_proxy=$http_proxy https_proxy=$https_proxy

RUN set -xe && \
        apt-get update && \
        apt-get install -y --no-install-recommends \
          git \
          grep \
          tar \
          make \
          perl-base \
          wget \
          xz-utils && \
        rm -rf /var/lib/apt && \
        wget -nv -O arduino.tar.xz http://downloads.arduino.cc/arduino-${ARDUINO_VER}.tar.xz &&\
        mkdir -p ${ARDUINO_DIR} && \
        tar xJC ${ARDUINO_DIR} --strip-components=1 -f arduino.tar.xz && \
        rm arduino.tar.xz && \
        git clone --depth=1 https://github.com/esp8266/Arduino.git \
          ${ARDUINO_DIR}/hardware/esp8266com/esp8266 && \
        cd ${ARDUINO_DIR}/hardware/esp8266com/esp8266 && \
        git submodule update --init && \
        cd tools && python get.py && \
        git clone --depth=1 https://github.com/plerup/makeEspArduino.git \
          /usr/local/src/makeEspArduino && \
        pip install pyserial && \
        mkdir -p ${ARDUINO_DIR}/hardware/espressif/esp32 && \
        git clone https://github.com/espressif/arduino-esp32.git \
          ${ARDUINO_DIR}/hardware/espressif/esp32 && \
        cd ${ARDUINO_DIR}/hardware/espressif/esp32 && \
        git submodule update --init --recursive && \
        cd tools && python get.py
#RUN set -xe && \
#        apt-get update && \
#        apt-get install -y --no-install-recommends \
#          wget \
#          xz-utils \
#        git && \
#        rm -rf /var/lib/apt && \
#        wget -nv -O arduino.tar.xz http://downloads.arduino.cc/arduino-${ARDUINO_VER}.tar.xz &&\
#        mkdir -p ${ARDUINO_DIR} && \
#        tar xJC ${ARDUINO_DIR} --strip-components=1 -f arduino.tar.xz && \
#        git clone --depth=1 https://github.com/esp8266/Arduino.git \
#          ${ARDUINO_DIR}/hardware/esp8266com/esp8266 && \
#        cd ${ARDUINO_DIR}/hardware/esp8266com/esp8266 && \
#        git submodule update --init && \
#        cd tools && python get.py && \
#        git clone --depth=1 https://github.com/plerup/makeEspArduino.git \
#          /usr/local/src/makeEspArduino && \
#        pip install pyserial && \
#        mkdir -p ${ARDUINO_DIR}/hardware/espressif/esp32 && \
#        git clone https://github.com/espressif/arduino-esp32.git \
#          ${ARDUINO_DIR}/hardware/espressif/esp32 && \
#        cd ${ARDUINO_DIR}/hardware/espressif/esp32 && \
#        git submodule update --init --recursive && \
#        cd tools && python get.py
#
#RUN -x && \
#        apk add --no-cache --virtual .fetch-deps tar xz && \
#        wget -O python.tar.xz $PYLINK && \
#        tar xJf python.tar.xz && \
#        rm -rf python.tar.xz && \
#        apk add --no-cache --virtual .build-deps \
#        bzip2-dev \
#        coreutils \
#        dpkg-dev dpkg \
#
