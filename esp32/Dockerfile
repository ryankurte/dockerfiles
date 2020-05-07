FROM debian:latest

RUN apt-get update -y && apt-get install -y \
    gcc cmake git wget make libncurses-dev flex \
    bison gperf python python-pip python-setuptools \
    python-serial python-cryptography python-future \
    protobuf-compiler protobuf-c-compiler python-protobuf \
    zsh vim libusb-dev

# Setup ESP IDF directory
WORKDIR /root

ENV IDF_PATH="/root/esp-idf/"
ARG IDF_VERSION=v4.2-dev
ARG IDF_SOURCE=https://github.com/espressif/esp-idf.git

# Clone the IDF
RUN git clone -b ${IDF_VERSION} --recursive ${IDF_SOURCE}

LABEL idf_version=${IDF_VERSION}
LABEL idf_source=${IDF_SOURCE}

# Apply patch for virtualenv 
# (see: https://github.com/espressif/esp-idf/issues/4744#issuecomment-594475740)
COPY 4744-virtualenv.patch esp-idf
RUN git -C esp-idf apply 4744-virtualenv.patch 

# Patch to return info for issue 5133
#COPY 5133-check-deps.patch esp-idf
#RUN git -C esp-idf apply 5133-check-deps.patch 

# Install the toolchain
ENV PATH="$PATH:/root/.local/bin"
RUN /root/esp-idf/install.sh

# Install dependencies
RUN python -m pip install --user -r /root/esp-idf/requirements.txt

# Install missed dependencies?
RUN python -m pip install --user pygdbmi==0.9.0.2 gdbgui

# Setup paths
ENV PATH="$PATH:/root/esp-idf/tools/"
ENV PATH="$PATH:/root/.espressif/tools/xtensa-esp32-elf/esp-2019r2-8.2.0/xtensa-esp32-elf/bin/"
ENV LC_ALL=C

# Setup working directory
RUN mkdir /root/work
WORKDIR /root/work

# Setup entrypoint to configure paths etc.
COPY entrypoint.sh /root/esp_idf/entrypoint.sh
ENTRYPOINT [ "/root/esp_idf/entrypoint.sh" ]

# Launch shell
CMD ["zsh"]

