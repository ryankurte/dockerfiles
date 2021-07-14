FROM espressif/idf:v4.2

Label Maintainer="Ryan Kurte <ryankurte@gmail.com>"
LABEL Description="IDF wrapper with protobuf compiler"

RUN apt-get update && apt-get install -y \
  python3 \
  python3-dev \
  python3-pip \
  libprotobuf-dev \
  protobuf-compiler \
  libprotobuf-c-dev \
  protobuf-c-compiler \
  python3-protobuf
