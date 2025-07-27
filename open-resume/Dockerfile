FROM cgr.dev/chainguard/git:latest AS git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/xitanggg/open-resume.git .

FROM gcr.io/distroless/nodejs22-debian12t AS builder
WORKDIR /app
COPY --from=git_clone --chown=node:node /git_clone/ /app/
RUN npm install --include=dev
RUN npm run build

FROM gcr.io/distroless/nodejs22-debian12 AS runner
WORKDIR /app
COPY --from=builder /app/.next/standalone .
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next/static ./.next/static

EXPOSE 3000
CMD ["server.js"]
