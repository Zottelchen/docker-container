FROM bitnami/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/Giingu/Enhanced-TTVDropBot.git .

FROM node:16-buster-slim as compiler
WORKDIR /usr/src/app
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends gnutls-bin git ca-certificates
COPY . .
RUN npm install
RUN npm run build

FROM node:16-buster-slim as runner
WORKDIR /usr/src/app/
COPY --from=compiler /usr/src/app/package*.json ./
COPY --from=compiler /usr/src/app/build ./build
RUN npm ci --production
RUN npm cache clean --force
RUN npm install
ENV NODE_ENV="production"
CMD [ "npm", "start" ]