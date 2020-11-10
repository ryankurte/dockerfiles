FROM debian:latest
MAINTAINER Ryan Kurte <ryankurte@gmail.com>
LABEL Description="Docker image for building x86/64 native projects"

ENV DEBIAN_FRONTEND=noninteractive

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
  libprotobuf-c-dev \
  protobuf-compiler \
  protobuf-c-compiler \
  python3-protobuf \
  && apt-get clean && rm -rf /var/lib/apt /tmp/* /var/tmp/*
  

# Update PIP & Install useful packages
RUN pip3 install pystache pyyaml


