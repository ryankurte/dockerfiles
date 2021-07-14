FROM ghcr.io/ryankurte/debian:latest
LABEL Maintainer="Ryan Kurte <ryankurte@gmail.com>"
LABEL Description="Docker image for building latex projects"

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y make latexmk pandoc texlive-full && \
    apt-get clean && \
    rm -rf /var/lib/apt

