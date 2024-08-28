FROM cgr.dev/chainguard/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://codeberg.org/proxigram/proxigram.git .

FROM node:18-alpine AS build-env
WORKDIR /app
COPY --from=git_clone /git_clone/package.json ./

ENV PNPM_HOME="/pnpm"
ENV PATH="$PNPM_HOME:$PATH"
RUN corepack enable

RUN pnpm install

COPY --from=git_clone /git_clone/ .

ENV NEXT_TELEMETRY_DISABLED=1
# Set environment variables
ENV URL="http://127.0.0.1:3000"
ENV RSS="true"
ENV CACHE="true"
ENV PROXY="true"
ENV REDIS_URL="redis:6379"
ENV ITEMS_PER_RSS="12"
ENV FETCH_PROVIDERS="true"
ENV PROVIDERS_LIST_URL="https://codeberg.org/ThePenguinDev/proxigram-providers/raw/branch/main/providers.json"
ENV EXPIRE_TIME_FOR_RSS="1d"
ENV EXPIRE_TIME_FOR_POST="1d"
ENV FETCH_PROVIDERS_EVERY="12h"
ENV EXPIRE_TIME_FOR_POSTS="1d"
ENV SLEEP_TIME_PER_REQUEST="555"
ENV USE_HEADLESS_PROVIDERS="false"
ENV EXPIRE_TIME_FOR_STORIES="1d"
ENV EXPIRE_TIME_FOR_PROFILE="1d"

RUN pnpm run build

FROM gcr.io/distroless/nodejs18-debian11:nonroot
WORKDIR /app
ENV NEXT_TELEMETRY_DISABLED=1

COPY --from=build-env /app/next.config.mjs ./
COPY --from=build-env /app/env.mjs ./
COPY --from=build-env /app/.git /app/.git
COPY --from=build-env /app/.next /app/.next
COPY --from=build-env /app/node_modules /app/node_modules
COPY --from=build-env /app/public /app/public

EXPOSE 3000

CMD ["./node_modules/next/dist/bin/next", "start"]
