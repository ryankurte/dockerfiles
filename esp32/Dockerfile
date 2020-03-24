FROM debian:latest

RUN apt-get update -y && apt-get install -y \
    gcc cmake git wget make libncurses-dev flex \
    bison gperf python python-pip python-setuptools \
    python-serial python-cryptography python-future \
    zsh vim

# Setup ESP IDF directory
WORKDIR /root

# Clone the IDF
RUN git clone -b v4.2-dev --recursive https://github.com/espressif/esp-idf.git

COPY idf-venv.patch .
RUN cd esp-idf && patch tools/idf_tools.py ../idf-venv.patch

# Install the toolchain
ENV PATH="$PATH:/root/.local/bin"
RUN /root/esp-idf/install.sh

# Install dependencies
RUN python -m pip install --user -r /root/esp-idf/requirements.txt

# Setup paths
ENV IDF_PATH="/root/esp-idf/"
ENV PATH="$PATH:/root/esp-idf/tools/"
ENV PATH="$PATH:/root/.espressif/tools/xtensa-esp32-elf/esp32-2019r2-8.2.0/xtensa-esp32-elf/bin/"

# Setup working directory
RUN mkdir /root/work
WORKDIR /root/work

# Launch shell
CMD ["zsh"]

