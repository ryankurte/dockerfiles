FROM espressif/idf:v4.2

Label Maintainer="Ryan Kurte <ryankurte@gmail.com>"
LABEL Description="IDF wrapper with protobuf compiler and other useful tools"

ENV PROTO_VER=3.17.3

RUN apt-get update && apt-get install -y \
  cmake \
  python3 \
  python3-dev \
  python3-pip && \
  apt-get clean && \
  rm -rf /var/lib/apt

# Set python3 as default
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 5

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

