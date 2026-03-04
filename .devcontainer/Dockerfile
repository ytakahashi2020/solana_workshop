FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

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
    ca-certificates \
    gnupg \
    && rm -rf /var/lib/apt/lists/*

# Install Node.js 22 LTS via NodeSource (as root)
RUN mkdir -p /etc/apt/keyrings && \
    curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg && \
    echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_22.x nodistro main" > /etc/apt/sources.list.d/nodesource.list && \
    apt-get update && \
    apt-get install -y nodejs && \
    rm -rf /var/lib/apt/lists/*

# Enable corepack and install pnpm / yarn
RUN corepack enable && \
    npm install -g yarn

# Switch to vscode user for user-level installations
USER vscode
ENV HOME=/home/vscode

# Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH="/home/vscode/.cargo/bin:${PATH}"

# Install Solana CLI
RUN curl -sSfL https://release.anza.xyz/stable/install | sh
ENV PATH="/home/vscode/.local/share/solana/install/active_release/bin:${PATH}"

# Generate default keypair
RUN solana-keygen new --no-bip39-passphrase --silent

# Install Anchor via AVM
RUN cargo install --git https://github.com/coral-xyz/anchor avm --force && \
    avm install 0.30.1 && \
    avm use 0.30.1
ENV PATH="/home/vscode/.avm/bin:${PATH}"

WORKDIR /workspaces
