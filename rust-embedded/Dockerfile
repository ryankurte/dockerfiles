FROM debian:stretch

# Install deps
RUN dpkg --add-architecture armhf && \
    apt update -y && \
    apt install -y cmake curl file build-essential libc6-i386 gcc-arm-linux-gnueabihf libc6-armhf-cross mingw-w64 gcc-mingw-w64 \
	libc6-dev-armhf-cross libssl-dev libssl-dev:armhf python3 python3-pip pkg-config libusb-dev libusb-1.0 && \
    apt install -y libusb-dev:armhf libusb-1.0:armhf && \ 
    rm -rf /var/lib/apt/lists

# Install rustup
RUN curl https://sh.rustup.rs -s > /home/install.sh && \
    chmod +x /home/install.sh && \
    sh /home/install.sh -y --verbose
ENV PATH "/root/.cargo/bin:$PATH"

# Setup rust
RUN rustup toolchain install nightly && \
    rustup default nightly && \
    rustup target add armv7-unknown-linux-gnueabihf thumbv7m-none-eabi thumbv7em-none-eabi thumbv7em-none-eabihf x86_64-apple-darwin i686-pc-windows-gnu & \
    cargo install cargo-deb && \
    cargo install sccache --features all && \
    cargo install cargo-watch

# Install AWS tools
RUN pip3 install awscli

