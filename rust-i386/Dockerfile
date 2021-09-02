FROM ghcr.io/ryankurte/debian:latest
LABEL Description="Container for cross-compiling i386 linux applications"

# Install deps
RUN dpkg --add-architecture i386 && \
    apt update -y && \
    apt install -y git cmake curl file automake make python3 python3-pip pkg-config libssl-dev \
        libc6-i386 libc6-dev-i386 libc6-dev-i386-cross libc6-i386-cross libssl-dev:i386 libusb-1.0-0:i386 libusb-1-dev:i386 && \ 
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
RUN rustup target add i686-unknown-linux-gnu

