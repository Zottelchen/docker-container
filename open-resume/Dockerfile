FROM bitnami/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/xitanggg/open-resume.git .

FROM node:18-alpine as builder
WORKDIR /app
COPY --from=git_clone /git_clone/ /app/
RUN npm install --include=dev
RUN npm run build

FROM cgr.dev/chainguard/node-lts AS runner
WORKDIR /app
COPY --from=builder /app/.next/standalone .
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next/static ./.next/static

EXPOSE 3000
CMD ["node", "server.js"]