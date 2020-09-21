FROM ubuntu:latest
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

# Set working directory for manually installed components
WORKDIR /root

# Install Golang
RUN curl -O https://storage.googleapis.com/golang/go1.12.4.linux-amd64.tar.gz \
    && tar -C /usr/local -xf go1.12.4.linux-amd64.tar.gz
ENV PATH $PATH:/usr/local/go/bin
RUN mkdir /root/go
ENV GOPATH /root/go


