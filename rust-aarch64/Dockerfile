FROM ghcr.io/ryankurte/debian:latest
LABEL Description="Container for cross-compiling arm64 linux applications"

# Install deps
RUN dpkg --add-architecture arm64 && \
    apt update -y && \
    apt install -y git cmake curl file automake make python3 python3-pip pkg-config libssl-dev \
        gcc-aarch64-linux-gnu libc6-dev-arm64-cross libc6-arm64-cross \
	libssl-dev:arm64 libusb-1.0-0:arm64 libsdl2-dev:arm64 libdbus-1-dev:arm64 && \ 
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
RUN rustup target add aarch64-unknown-linux-gnu

