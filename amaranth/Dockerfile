FROM ghcr.io/ryankurte/base:latest

# Install deps
RUN apt-get update && apt-get install -y \
	libboost-all-dev libeigen3-dev \
	build-essential clang bison flex \
	libreadline-dev gawk tcl-dev libffi-dev git \
	graphviz xdot pkg-config python3 libboost-system-dev \
	libboost-python-dev libboost-filesystem-dev zlib1g-dev \
	libhidapi-dev libusb-1.0-0-dev

# Install project trellis
RUN git clone --recursive https://github.com/YosysHQ/prjtrellis.git && \
	cd prjtrellis/libtrellis && \
	cmake -DCMAKE_INSTALL_PREFIX=/usr/local . && \
	make -j install

# Install nextpnr
RUN git clone --recursive https://github.com/YosysHQ/nextpnr.git && \
	cd nextpnr && \
	cmake . -DARCH="ecp5" -DTRELLIS_INSTALL_PREFIX=/usr/local && \
	make -j install


# Install yosys
RUN git clone --recursive https://github.com/YosysHQ/yosys && \
	cd yosys && \
	make -j install

# Install amaranth
COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

# Install icesprog
RUN git clone https://github.com/wuxx/icesugar.git && \
	cd icesugar/tools/src && \
	make && \
	cp ./icesprog /usr/local/bin/
	
