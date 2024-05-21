FROM cgr.dev/chainguard/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://codeberg.org/lamacchinadesiderante/proxyraye.git .

FROM cgr.dev/chainguard/node:latest AS build
ENV NEXT_TELEMETRY_DISABLED 1
ENV NEXT_PRIVATE_STANDALONE true
WORKDIR /app
COPY --from=git_clone /git_clone/package.json /git_clone/package-lock.json /app/
RUN rm -rf node_modules && npm ci
COPY --from=git_clone --chown=node:node /git_clone/ /app/
RUN npm run build

FROM cgr.dev/chainguard/node:latest AS runner
ENV NEXT_TELEMETRY_DISABLED 1
ENV NODE_ENV production
WORKDIR /app
COPY --from=build /app/.next/standalone .
COPY --from=build /app/.next/static ./.next/static
COPY --from=build /app/public ./public

EXPOSE 3000

CMD ["server.js"]