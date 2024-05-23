FROM cgr.dev/chainguard/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/valeriansaliou/sonic.git .

FROM rust:1.77.2-slim-bullseye AS build

RUN apt-get update
RUN apt-get install -y build-essential clang git

RUN rustup --version
RUN rustup component add rustfmt

RUN rustc --version && \
    rustup --version && \
    cargo --version

WORKDIR /app
COPY --from=git_clone /git_clone/ .

RUN cargo clean && cargo build --release
RUN strip ./target/release/sonic

FROM gcr.io/distroless/cc

WORKDIR /usr/src/sonic

COPY --from=build /app/target/release/sonic /usr/local/bin/sonic

CMD [ "sonic", "-c", "/etc/sonic.cfg" ]

EXPOSE 1491