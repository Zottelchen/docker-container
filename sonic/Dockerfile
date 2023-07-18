FROM rust:slim-bullseye AS build

RUN apt-get update
RUN apt-get install -y build-essential clang git

RUN rustup --version
RUN rustup component add rustfmt

RUN rustc --version && \
    rustup --version && \
    cargo --version

WORKDIR /app
RUN git clone --depth 1 https://github.com/valeriansaliou/sonic.git .
RUN cargo clean && cargo build --release --target aarch64-unknown-linux-gnu
RUN strip ./target/aarch64-unknown-linux-gnu/release/sonic

FROM gcr.io/distroless/cc

WORKDIR /usr/src/sonic

COPY --from=build /app/target/aarch64-unknown-linux-gnu/release/sonic /usr/local/bin/sonic

CMD [ "sonic", "-c", "/etc/sonic.cfg" ]

EXPOSE 1491