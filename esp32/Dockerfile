FROM debian:latest

RUN apt-get update -y && apt-get install -y \
    gcc git wget make libncurses-dev flex \
    bison gperf python python-pip python-setuptools \
    python-serial python-cryptography python-future

# Setup ESP IDF directory
RUN mkdir /root/esp
WORKDIR /root/esp

# Clone the IDF
RUN git clone -b v3.2.2 --recursive https://github.com/espressif/esp-idf.git

# Download the toolchain
RUN wget https://dl.espressif.com/dl/xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz && \
    tar -xzf xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz && \
    export PATH="/root/esp/xtensa-esp32-elf/bin:$PATH"


