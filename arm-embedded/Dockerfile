FROM ghcr.io/ryankurte/debian:latest
LABEL Maintainer="Ryan Kurte <ryankurte@gmail.com>"
LABEL Description="Docker image for building arm-embedded projects"

ENV PROTO_VER=3.17.3

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
  ninja-build \
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
  clang-tidy \
  build-essential \
  python3 \
  python3-dev \
  python3-setuptools \
  python3-pip \
  python3-serial \
  gcc-arm-none-eabi \
  gcc-arm-linux-gnueabihf \
  gdb-multiarch \
  srecord \
  wget

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

# Install protobufs
RUN mkdir /tmp/protobufs && cd /tmp/protobufs && \
  wget https://github.com/protocolbuffers/protobuf/releases/download/v$PROTO_VER/protoc-$PROTO_VER-linux-x86_64.zip && \
  unzip protoc-$PROTO_VER-linux-x86_64.zip && \
  mv include/* /usr/local/include/ && \
  mv bin/* /usr/local/bin/ && \
  cd / && rm -rf /tmp/protobufs

# Update PIP & Install useful packages
RUN pip3 install protobuf grpcio-tools awscli

# Install codechecker
RUN pip3 install --user codechecker
ENV PATH=/root/.local/bin:$PATH

# Cleanup
RUN apt-get clean && \
  rm -rf /var/lib/apt
