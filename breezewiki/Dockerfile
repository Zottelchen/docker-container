FROM debian:13-slim AS base

WORKDIR /app

RUN apt-get update -y
RUN apt-get install -y --no-install-recommends ca-certificates curl racket git sqlite3 libfontconfig1 libcairo2 libjpeg62-turbo libglib2.0-0 libpango-1.0-0 libpangocairo-1.0-0

RUN git clone --depth=1 https://gitdab.com/cadence/breezewiki.git .
RUN raco pkg install --batch --auto --no-docs --skip-installed req-lib && \
    raco req -d
RUN raco exe dist.rkt
RUN touch config.ini && \
    raco distribute breezewiki dist && \
    ls -al /app/breezewiki/ && \
    rm config.ini
WORKDIR /app/breezewiki
RUN mv ./lib/plt/dist/exts/ert/r0/app/config.ini ./config.ini && ln -s /app/config.ini ./lib/plt/dist/exts/ert/r0/app/config.ini

FROM debian:13-slim AS libprovider
WORKDIR /tmp
RUN apt-get update -y && \
    apt-get download zlib1g liblz4-1 sqlite3 && \
    mkdir /dpkg && \
    for deb in *.deb; do dpkg --extract "$deb" /dpkg || exit 10; done

FROM gcr.io/distroless/base-debian13:latest as final
WORKDIR /app
COPY --from=libprovider /dpkg /
COPY --from=base /app/breezewiki /app/
EXPOSE 10416
CMD ["/app/bin/dist"]