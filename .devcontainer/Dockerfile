FROM mcr.microsoft.com/devcontainers/typescript-node:1-22-bookworm

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        openssl \
        curl \
        wget \
        git \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Enable Corepack and activate pnpm
RUN corepack enable \
    && corepack prepare pnpm@latest --activate

# Configure pnpm global directory
ENV PNPM_HOME=/home/node/.local/share/pnpm
ENV PATH=$PNPM_HOME:$PATH

RUN mkdir -p $PNPM_HOME \
    && chown -R node:node /home/node/.local

# Shopify CLI
USER node
RUN pnpm add -g @shopify/cli@latest

USER node