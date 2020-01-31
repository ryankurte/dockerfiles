from debian:latest

# Fetch dependencies
RUN apt update && apt-get install -y \
  build-essential \
  clang \
  llvm \
  make \
  git \
  gnat \
  zlib1g \
  zlib1g-dev \
  vim \
  zsh

# Fetch source
RUN git clone https://github.com/ghdl/ghdl.git --depth=1 --branch v0.36

# Build ghdl
RUN cd ghdl && ./configure --with-llvm-config --prefix=/usr/local && \
  make -j && \
  make install
  
