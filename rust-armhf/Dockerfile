FROM ghcr.io/ryankurte/debian:latest
LABEL Description="Container for cross-compiling armhf linux applications"

# Install deps
RUN dpkg --add-architecture armhf && \
    apt update -y && \
    apt install -y git cmake curl file automake make python3 python3-pip pkg-config libssl-dev \
        gcc-arm-linux-gnueabihf libc6-dev-armhf-cross libc6-armhf-cross \
	    libssl-dev:armhf libusb-1.0-0:armhf libusb-1.0-0-dev:armhf libsdl2-dev:armhf libdbus-1-3:armhf libdbus-1-dev:armhf && \ 
    rm -rf /var/lib/apt/lists

# Install rustup
RUN curl https://sh.rustup.rs -s > /home/install.sh && \
    chmod +x /home/install.sh && \
    sh /home/install.sh -y --verbose

ENV PATH "/root/.cargo/bin:$PATH"

# Setup rust
RUN rustup toolchain install nightly && \
    rustup default nightly && \
    cargo install --git https://github.com/mozilla/sccache.git --features all && \
    cargo install cargo-deb
RUN rustup target add armv7-unknown-linux-gnueabihf

