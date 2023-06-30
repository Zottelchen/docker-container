FROM debian:stable-slim AS base

WORKDIR /app
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends ca-certificates curl racket git  \
    && apt-get autoclean -y \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* \
    && git clone --depth=1 https://gitdab.com/cadence/breezewiki.git . \
    && raco pkg install --batch --auto --no-docs --skip-installed req-lib \
    && raco req -d

EXPOSE 10416
CMD ["racket", "dist.rkt"]
