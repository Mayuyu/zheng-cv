FROM rust:latest AS installer

RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
    --mount=type=cache,target=/var/lib/apt,sharing=locked \
    apt update && apt-get --no-install-recommends install -y \
    cmake \
    && rm -rf /var/lib/apt/lists/*
RUN cargo install tex-fmt starship

FROM texlive/texlive:latest

RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
    --mount=type=cache,target=/var/lib/apt,sharing=locked \
    apt update && apt-get --no-install-recommends install -y \
    openssh-client \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

COPY --from=installer /usr/local/cargo/bin/tex-fmt \
    /usr/local/cargo/bin/starship /usr/local/bin/

RUN echo 'eval "$(starship init bash)"' >> ~/.bashrc
