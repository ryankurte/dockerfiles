FROM ghcr.io/ryankurte/debian:latest
Label Maintainer="Ryan Kurte <ryankurte@gmail.com>"
LABEL Description="Docker image for building x86/64 native projects"

ENV DEBIAN_FRONTEND=noninteractive
ENV PROTO_VER=3.17.3

# General dependencies and cleanup
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
  build-essential \
  clang \
  python3 \
  python3-dev \
  python3-pip \
  python3-setuptools \
  libsodium-dev \
  libzmq3-dev \
  libczmq-dev \
  pkg-config \
  valgrind \
  cppcheck \
  wget \
  && apt-get clean && rm -rf /var/lib/apt /tmp/* /var/tmp/*

# Install protobufs
RUN mkdir /tmp/protobufs && cd /tmp/protobufs && \
  wget https://github.com/protocolbuffers/protobuf/releases/download/v$PROTO_VER/protoc-$PROTO_VER-linux-x86_64.zip && \
  unzip protoc-$PROTO_VER-linux-x86_64.zip && \
  mv include/* /usr/local/include/ && \
  mv bin/* /usr/local/bin/ && \
  cd / && rm -rf /tmp/protobufs

# Update PIP & Install useful packages
RUN pip3 install pystache pyyaml protobuf grpcio-tools


