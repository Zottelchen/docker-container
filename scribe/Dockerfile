FROM bitnami/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://git.sr.ht/~edwardloveall/scribe .

# Node build

FROM node:16 as node_build
WORKDIR /tmp_build

COPY --from=git_clone /git_clone/package.json .
COPY --from=git_clone /git_clone/yarn.lock .
RUN yarn install --no-progress --frozen-lockfile

COPY --from=git_clone /git_clone/webpack.mix.js .
COPY --from=git_clone /git_clone/src ./src
RUN yarn prod

# Crystal build

FROM debian:11-slim as lucky_build
RUN apt-get update -y
RUN apt-get install -y --no-install-recommends libc6-dev libevent-dev libpcre2-dev libpng-dev libssl-dev libyaml-dev zlib1g-dev git curl ca-certificates
WORKDIR /tmp_environment
ENV SKIP_LUCKY_TASK_PRECOMPILATION="1"
RUN curl -L https://crystal-lang.org/install.sh -o install.sh
RUN chmod +x install.sh && bash install.sh --version=1.8 && crystal -v
RUN git clone https://github.com/luckyframework/lucky_cli
WORKDIR /tmp_environment/lucky_cli
RUN git checkout v1.0.0
RUN shards install --without-development
RUN shards build --production && cp bin/lucky /usr/local/bin && lucky -v

WORKDIR /tmp_build
COPY --from=git_clone /git_clone/shard.* ./
RUN  shards install --production
COPY --from=git_clone /git_clone/. .
COPY --from=node_build /tmp_build/public/mix-manifest.json public/mix-manifest.json
RUN crystal build --static src/start_server.cr
RUN crystal build --static tasks.cr -o run_task

# Runner

FROM cgr.dev/chainguard/wolfi-base:latest

RUN adduser -D nonroot && addgroup nonroot nonroot
USER nonroot
WORKDIR /app
COPY --chown=nonroot:nonroot --from=node_build /tmp_build/public public
COPY --chown=nonroot:nonroot --from=lucky_build /tmp_build/start_server start_server
COPY --chown=nonroot:nonroot --from=lucky_build /tmp_build/run_task run_task
COPY --chown=nonroot:nonroot --from=git_clone /git_clone/script/docker_entrypoint ./

RUN mkdir ./config
RUN chown -R nonroot /app

CMD ["/app/docker_entrypoint"]