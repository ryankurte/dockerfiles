FROM debian:latest
MAINTAINER Ryan Kurte <ryankurte@gmail.com>
LABEL Description="Docker image for building arm-embedded projects"

RUN dpkg --add-architecture armhf

# General dependencies
RUN apt-get update && apt-get install -y \
  git \
  subversion \
  curl \
  cmake \
  make \
  automake \
  autoconf \
  python-setuptools \
  ninja-build \
  python-dev \
  libtool \
  unzip \
  libffi-dev \
  libssl-dev \
  libusb-1.0.0 \
  libusb-1.0.0-dev \
  software-properties-common \
  gawk \
  genromfs \
  ccache \
  clang \
  build-essential \
  python3 \
  python3-dev \
  python3-pip \
  libprotobuf-dev \
  protobuf-compiler \
  libprotobuf-c-dev \
  protobuf-c-compiler \
  python-protobuf \
  gcc-arm-none-eabi \
  gcc-arm-linux-gnueabihf \
  gdb-multiarch \
  mingw-w64 \
  gcc-mingw-w64
  

# Python tools
RUN pip3 install pyserial

# Rust and arm targets
RUN curl https://sh.rustup.rs -sSf | \
    sh -s -- --default-toolchain stable -y && \
    /root/.cargo/bin/rustup update nightly && \
    /root/.cargo/bin/rustup target add thumbv7m-none-eabi && \
    /root/.cargo/bin/rustup target add thumbv7em-none-eabi && \
    /root/.cargo/bin/rustup target add thumbv7em-none-eabihf
ENV PATH=/root/.cargo/bin:$PATH

# STLink util
RUN git clone https://github.com/texane/stlink.git && \
  cd stlink && mkdir build && cd build && \
  cmake .. && make && make install

# Cleanup
RUN apt-get clean && \
  rm -rf /var/lib/apt

