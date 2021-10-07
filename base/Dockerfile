FROM ghcr.io/ryankurte/debian:latest

LABEL Maintainer="Ryan Kurte <ryankurte@gmail.com>"
LABEL Description="Debian derived common / base image for dev tools"

ENV PROTO_VER=3.17.3

# Fetch common base packages via apt
RUN apt-get update -y && \
    apt-get install -y \
    vim git curl wget make cmake automake curl file pkg-config libtool \
    python3 python3-pip python3-dev python3-setuptools \
    libssl-dev libffi-dev libusb-1.0-0 libusb-1.0-0-dev libdbus-1-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists

# Install rust
RUN curl https://sh.rustup.rs -s > /home/install.sh && \
    chmod +x /home/install.sh && \
    sh /home/install.sh -y --verbose
ENV PATH "/root/.cargo/bin:$PATH"

# Install rust toolchain and utils
RUN rustup toolchain install nightly && \
    cargo install --git https://github.com/mozilla/sccache.git --features all && \
    cargo install cargo-deb && \
    cargo install cargo-binstall && \
    cargo install cross

# Install protobuf tooling
RUN mkdir /tmp/protobufs && cd /tmp/protobufs && \
  wget https://github.com/protocolbuffers/protobuf/releases/download/v$PROTO_VER/protoc-$PROTO_VER-linux-x86_64.zip && \
  unzip protoc-$PROTO_VER-linux-x86_64.zip && \
  mv include/* /usr/local/include/ && \
  mv bin/* /usr/local/bin/ && \
  cd / && rm -rf /tmp/protobufs
RUN pip3 install protobuf
