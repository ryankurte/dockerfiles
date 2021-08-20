FROM ghcr.io/ryankurte/debian:latest

Label Maintainer="Ryan Kurte <ryankurte@gmail.com>"
LABEL Description="IDF wrapper with protobuf compiler and other useful tools"

ENV PROTO_VER=3.17.3

RUN apt-get update && apt-get install -y \
  cmake bison make ninja-build ccache \
  ca-certificates check curl wget unzip xz-utils zip flex git gperf lcov \
  python3 python3-dev python3-pip python3-setuptools \
  libncurses-dev libffi-dev libssl-dev dfu-util libusb-1.0-0 && \
  apt-get clean && \
  rm -rf /var/lib/apt

# Set python3 as default
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 5

# Install the ESP IDF
# Via: https://github.com/espressif/esp-idf/blob/master/tools/docker/Dockerfile
ARG IDF_CLONE_URL=https://github.com/espressif/esp-idf.git
ARG IDF_CLONE_BRANCH_OR_TAG=v4.3
ARG IDF_CHECKOUT_REF=

ENV IDF_PATH=/opt/esp/idf
ENV IDF_TOOLS_PATH=/opt/esp

RUN echo IDF_CHECKOUT_REF=$IDF_CHECKOUT_REF IDF_CLONE_BRANCH_OR_TAG=$IDF_CLONE_BRANCH_OR_TAG && \
    git clone --recursive \
      ${IDF_CLONE_BRANCH_OR_TAG:+-b $IDF_CLONE_BRANCH_OR_TAG} \
      $IDF_CLONE_URL $IDF_PATH && \
    if [ -n "$IDF_CHECKOUT_REF" ]; then \
      cd $IDF_PATH && \
      git checkout $IDF_CHECKOUT_REF && \
      git submodule update --init --recursive; \
    fi

# Install all the required tools, plus CMake
RUN $IDF_PATH/tools/idf_tools.py --non-interactive install required \
  && $IDF_PATH/tools/idf_tools.py --non-interactive install cmake \
  && $IDF_PATH/tools/idf_tools.py --non-interactive install-python-env \
  && rm -rf $IDF_TOOLS_PATH/dist

# Ccache is installed, enable it by default
ENV IDF_CCACHE_ENABLE=1


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

COPY entrypoint.sh /opt/esp/entrypoint.sh

ENTRYPOINT [ "/opt/esp/entrypoint.sh" ]
CMD [ "/bin/bash" ]

