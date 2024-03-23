FROM mcr.microsoft.com/devcontainers/rust:1-1-bullseye as base

# ********************************************************
# * Anything else you want to do like clean up goes here *
# ********************************************************

# [Optional] Set the default user. Omit if you want to keep the default as root.

FROM base as dev
RUN apt-get update && apt-get install -y xz-utils libudev-dev

USER vscode
COPY Cargo.toml /tmp/
RUN awk -F' = ' '/ = /{print $2 " " $1}' /tmp/Cargo.toml | xargs -n2 -P$(nproc) cargo install --locked --version \
    && sudo rm -rf /tmp/Cargo.toml "$CARGO_HOME/registry"
