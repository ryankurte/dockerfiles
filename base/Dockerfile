FROM ghcr.io/ryankurte/debian:latest

LABEL Maintainer="Ryan Kurte <ryankurte@gmail.com>"
LABEL Description="Debian derived common / base image for dev tools"

RUN apt-get update -y && \
    apt-get install -y \
    vim git curl make pkg-config \
    python3 python3-pip python3-dev python3-setuptools \
    libprotobuf-c-dev protobuf-compiler protobuf-c-compiler python3-protobuf && \
    apt-get clean && \
    rm -rf /var/lib/apt
