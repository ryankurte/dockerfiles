FROM ghcr.io/ryankurte/debian:latest

# Install deps
RUN dpkg --add-architecture armhf &&\
    apt update -y && \
    apt install -y git cmake curl file build-essential libssl-dev python3 python3-pip pkg-config libusb-dev libusb-1.0 && \
    apt install -y libc6-dev-armhf-cross libc6-armhf-cross g++-arm-linux-gnueabihf gcc-arm-linux-gnueabihf libssl-dev:armhf libusb-dev:armhf libusb-1.0:armhf && \ 
    rm -rf /var/lib/apt/lists

# Install rustup
RUN curl https://sh.rustup.rs -s > /home/install.sh && \
    chmod +x /home/install.sh && \
    sh /home/install.sh -y --verbose

ENV PATH "/root/.cargo/bin:$PATH"

# Setup rust
RUN rustup toolchain install nightly && \
    rustup default nightly && \
    cargo install cargo-deb && \
    cargo install --git https://github.com/mozilla/sccache.git --features all && \
    cargo install cargo-watch
RUN rustup target add armv7-unknown-linux-gnueabihf aarch64-unknown-linux-gnu && \
    rustup target add thumbv7m-none-eabi thumbv7em-none-eabi thumbv7em-none-eabihf
