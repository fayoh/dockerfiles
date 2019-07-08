# Compilation container for STM8(s) development

This container is based on ubuntu rolling and contains:
* make
* sdcc 3.9.0 (amd64 version)
* libusb-1
* My stm8s header - master [github](https://github.com/fayoh/stm8s-util.git)
* stm8flash - master [github](https://github.com/vdudouyt/stm8flash.git)

# Building
Build the image with docker build like you normally do. Supply http_proxy and https_proxy as build arguments if needed.

# Running
As this is an image for development I like to keep the source/artifacts outside of the image. Make a bind mount to your code and make sure to run as your user to be able to use your results later. For flashing use the device option to access your serial device.

## Example
`docker run -it --rm --user=$(id -u ${USER}) -v /path/to/src:/mnt/src -w /mnt/src --device=/dev/ttyUSB0 stm8-dev make flash`
