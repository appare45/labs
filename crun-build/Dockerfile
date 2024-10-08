FROM ubuntu
RUN apt update && apt install -y build-essential pkg-config git autoconf libtool python3 libyajl-dev libcap-dev libseccomp-dev libsystemd-dev
WORKDIR /
RUN git clone https://github.com/containers/crun.git
WORKDIR /crun
RUN ./autogen.sh && ./configure && make
