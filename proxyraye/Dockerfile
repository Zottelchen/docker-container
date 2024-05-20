FROM bitnami/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://codeberg.org/lamacchinadesiderante/proxyraye.git .

FROM cgr.dev/chainguard/node:latest AS build
ENV NODE_ENV production
ENV NEXT_TELEMETRY_DISABLED 1
WORKDIR /app
COPY --from=git_clone /git_clone/package.json /git_clone/package-lock.json /app/
RUN npm ci
COPY --from=git_clone --chown=node:node /git_clone/ /app/
RUN npm run build

FROM cgr.dev/chainguard/node:latest AS runner
ENV NODE_ENV production
ENV NEXT_TELEMETRY_DISABLED 1
WORKDIR /app
COPY --from=build /app/package.json .
COPY --from=build /app/next.config.js .
COPY --from=build /app/public ./public
COPY --from=build /app/node_modules ./node_modules
COPY --from=build /app/.next/ ./.next

EXPOSE 3000

ENTRYPOINT [ "/usr/bin/npm" ]
CMD ["run", "start"]