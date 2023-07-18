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
RUN if [ "$TARGETPLATFORM" = "linux/arm64/v8" ]; \
    then export RUST_TARGET=aarch64-unknown-linux-gnu; \
    else export RUST_TARGET=x86_64-unknown-linux-gnu; \
    fi && \
    cargo clean && cargo build --release --target $RUST_TARGET
RUN strip ./target/x86_64-unknown-linux-gnu/release/sonic

FROM gcr.io/distroless/cc

WORKDIR /usr/src/sonic

COPY --from=build /app/target/x86_64-unknown-linux-gnu/release/sonic /usr/local/bin/sonic

CMD [ "sonic", "-c", "/etc/sonic.cfg" ]

EXPOSE 1491