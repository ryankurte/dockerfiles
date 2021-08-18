Label Maintainer="Ryan Kurte <ryankurte@gmail.com>"
LABEL Description="WASM tools"

ENV DEBIAN_FRONTEND=noninteractive

# Build C dependencies
FROM ghcr.io/ryankurte/debian:latest

# General dependencies and cleanup
RUN apt-get update && apt-get install -y \
  git \
  curl \
  cmake \
  make \
  libtool \
  unzip \
  libffi-dev \
  libssl-dev \
  software-properties-common \
  build-essential \
  clang \
  python3 \
  python3-dev \
  python3-pip \
  pkg-config \
  && apt-get clean && rm -rf /var/lib/apt /tmp/* /var/tmp/*
  
# Build binaryen
RUN git clone https://github.com/WebAssembly/binaryen.git && \
  cd binaryen && mkdir build && cd build && cmake .. && make -j

# Build wabt
RUN git clone https://github.com/WebAssembly/wabt.git && \
  cd wabt && git submodule update --init --recursive && \
  mkdir build && cd build && cmake .. && make -j

# TODO: Build wasm-tools? requires rust, maybe worth multistage eh.



