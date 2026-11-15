FROM golang:1.27.4-bookworm AS go
FROM eclipse-temurin:25.0.4_7-jdk-noble AS java
FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates curl git build-essential gcc-13 make maven \
    libgmp-dev libffi-dev libnuma-dev libncurses-dev pkg-config xz-utils \
    && rm -rf /var/lib/apt/lists/*
COPY --from=go /usr/local/go /usr/local/go
COPY --from=java /opt/java/openjdk /opt/java/openjdk
ENV JAVA_HOME=/opt/java/openjdk
ENV PATH=/opt/java/openjdk/bin:/usr/local/go/bin:/root/.cargo/bin:/root/.ghcup/bin:${PATH}
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs -o /tmp/rustup.sh \
    && sh /tmp/rustup.sh -y --profile minimal --default-toolchain 1.100.0 --component rustfmt \
    && rm /tmp/rustup.sh
ENV BOOTSTRAP_HASKELL_NONINTERACTIVE=1 \
    BOOTSTRAP_HASKELL_MINIMAL=1
RUN curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org -o /tmp/ghcup.sh \
    && sh /tmp/ghcup.sh \
    && ghcup install ghc 9.12.4 --set \
    && ghcup install cabal 3.16.0.0 --set \
    && rm /tmp/ghcup.sh
WORKDIR /workspace
