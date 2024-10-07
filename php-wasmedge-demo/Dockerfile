FROM ubuntu:jammy
WORKDIR /opt
RUN apt update && apt install -y git curl wget make build-essential autoconf bison re2c pkg-config sqlite libsqlite3-dev

RUN DEBIAN_FRONTEND=noninteractive TZ=Asia/Tokyo apt install -y tcl
# https://github.com/WebAssembly/wasi-sdk?tab=readme-ov-file#install
RUN WASI_OS=linux \
  WASI_VERSION=24 \
  WASI_ARCH=$(uname -m) \
  WASI_VERSION_FULL=${WASI_VERSION}.0 && \
  wget https://github.com/WebAssembly/wasi-sdk/releases/download/wasi-sdk-${WASI_VERSION}/wasi-sdk-${WASI_VERSION_FULL}-${WASI_ARCH}-${WASI_OS}.tar.gz && \
  tar xvf wasi-sdk-${WASI_VERSION_FULL}-${WASI_ARCH}-${WASI_OS}.tar.gz
RUN git clone --depth=1 -b php-wasmedge-demo \
   https://github.com/vmware-labs/webassembly-language-runtimes.git wlr-demo
WORKDIR /opt/wlr-demo
RUN WASI_OS=linux \
  WASI_VERSION=24 \
  WASI_ARCH=$(uname -m) \
  WASI_VERSION_FULL=${WASI_VERSION}.0 \
  WASI_SDK_ROOT=/opt/wasi-sdk-${WASI_VERSION_FULL}-${WASI_ARCH}-${WASI_OS}\
  WASMLABS_RUNTIME=wasmedge\
  ./wl-make.sh php/php-7.4.32/ && tree build-output/php/php-7.4.32/bin/

