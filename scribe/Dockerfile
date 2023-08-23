FROM bitnami/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://git.sr.ht/~edwardloveall/scribe .

# Node build

FROM node:16 as node_build
WORKDIR /tmp_build

COPY --from=git_clone /git_clone/package.json .
COPY --from=git_clone /git_clone/yarn.lock .
RUN yarn install --no-progress --frozen-lockfile --network-timeout 600000

COPY --from=git_clone /git_clone/webpack.mix.js .
COPY --from=git_clone /git_clone/src ./src
RUN yarn prod

# Crystal build

FROM 84codes/crystal:1.8.2-debian-11 as lucky_build
WORKDIR /tmp_environment
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
RUN mkdir ./config

# Runner

FROM gcr.io/distroless/base-debian11:latest

WORKDIR /app
COPY --from=node_build /tmp_build/public public
COPY --from=lucky_build /tmp_build/start_server start_server
COPY --from=lucky_build /tmp_build/run_task run_task
COPY --from=git_clone /git_clone/script/docker_entrypoint ./
COPY --from=lucky_build /tmp_build/config/. /app/config/

CMD ["/app/docker_entrypoint"]