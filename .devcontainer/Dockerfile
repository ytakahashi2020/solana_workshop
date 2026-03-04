FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# Version arguments
ARG NODE_MAJOR=22
ARG ANCHOR_VERSION="0.30.1"

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    pkg-config \
    libudev-dev \
    libssl-dev \
    curl \
    wget \
    git \
    jq \
    && rm -rf /var/lib/apt/lists/*

# Switch to vscode user for all installations
USER vscode

# Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH="/home/vscode/.cargo/bin:${PATH}"

# Install Solana CLI (Agave)
RUN sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)"
ENV PATH="/home/vscode/.local/share/solana/install/active_release/bin:${PATH}"

# Generate default keypair for solana-test-validator
RUN solana-keygen new --no-bip39-passphrase --silent

# Install Anchor via AVM
RUN cargo install --git https://github.com/coral-xyz/anchor avm --force && \
    avm install ${ANCHOR_VERSION} && \
    avm use ${ANCHOR_VERSION}
ENV PATH="/home/vscode/.avm/bin:${PATH}"

# Switch back to root for Node.js installation
USER root

# Install Node.js LTS
RUN curl -fsSL https://deb.nodesource.com/setup_${NODE_MAJOR}.x | bash - && \
    apt-get install -y nodejs && \
    rm -rf /var/lib/apt/lists/*

# Enable corepack and install pnpm
RUN corepack enable && corepack prepare pnpm@latest --activate

# Install yarn globally (some Anchor templates use it)
RUN npm install -g yarn

# Switch back to vscode user
USER vscode

WORKDIR /workspaces
