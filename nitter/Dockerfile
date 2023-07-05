FROM debian:11-slim AS base

WORKDIR /app
RUN echo 'deb http://deb.debian.org/debian bullseye-backports main' > /etc/apt/sources.list.d/backports.list
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends gcc git libc6-dev libsass-dev nim/bullseye-backports libpcre2-dev ca-certificates  && \
    apt-get autoclean -y && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*
RUN git clone --depth=1 https://github.com/zedeus/nitter.git . && \
    nimble install -y --depsOnly && \
    nimble build -d:danger -d:lto -d:strip && \
    nimble scss && \
    nimble md

FROM debian:11-slim AS libprovider
WORKDIR /tmp
RUN apt-get update -y && \
    apt-get download libpcre3 && \
    mkdir /dpkg && \
    for deb in *.deb; do dpkg --extract "$deb" /dpkg || exit 10; done

FROM gcr.io/distroless/base-debian11:latest as final
WORKDIR /app
COPY --from=libprovider /dpkg /
COPY --from=base /app/nitter /app/
COPY --from=base /app/nitter.example.conf /app/nitter.conf
COPY --from=base /app/public /app/public
EXPOSE 8080
CMD ["/app/nitter"]