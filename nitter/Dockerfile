FROM bitnami/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/zedeus/nitter.git .

FROM debian:12-slim AS base
WORKDIR /app
RUN apt-get update -y
RUN apt-get install -y --no-install-recommends gcc git libc6-dev libsass-dev nim libpcre2-dev ca-certificates

COPY --from=git_clone /git_clone/nitter.nimble .
RUN nimble install -y --depsOnly
COPY --from=git_clone /git_clone /app
RUN nimble build -d:danger -d:lto -d:strip
RUN nimble scss && \
    nimble md

FROM debian:12-slim AS libprovider
WORKDIR /tmp
RUN apt-get update -y && \
    apt-get download libpcre3 && \
    mkdir /dpkg && \
    for deb in *.deb; do dpkg --extract "$deb" /dpkg || exit 10; done

FROM gcr.io/distroless/base-debian12:latest as final
WORKDIR /app
COPY --from=libprovider /dpkg /
COPY --from=base /app/nitter /app/
COPY --from=base /app/nitter.example.conf /app/nitter.conf
COPY --from=base /app/public /app/public
EXPOSE 8080
CMD ["/app/nitter"]