
## Fetch Calckey
FROM alpine:3.18 as fetch
WORKDIR /calckey
RUN apk add --no-cache --no-progress git
RUN git clone --depth 1 https://codeberg.org/calckey/calckey.git .


## Install dev and compilation dependencies, build files
FROM alpine:3.18 as build
WORKDIR /calckey

# Install compilation dependencies
RUN apk add --no-cache --no-progress git alpine-sdk python3 nodejs-current npm rust cargo vips tree

# Copy only the cargo dependency-related files first, to cache efficiently
COPY --from=fetch /calckey/packages/backend/native-utils/Cargo.toml packages/backend/native-utils/Cargo.toml
COPY --from=fetch /calckey/packages/backend/native-utils/Cargo.lock packages/backend/native-utils/Cargo.lock
COPY --from=fetch /calckey/packages/backend/native-utils/src/lib.rs packages/backend/native-utils/src/
COPY --from=fetch /calckey/packages/backend/native-utils/migration/Cargo.toml packages/backend/native-utils/migration/Cargo.toml
COPY --from=fetch /calckey/packages/backend/native-utils/migration/src/lib.rs packages/backend/native-utils/migration/src/

# Install cargo dependencies
RUN tree && cargo fetch --locked --manifest-path /calckey/packages/backend/native-utils/Cargo.toml

# Copy only the dependency-related files first, to cache efficiently
COPY --from=fetch /calckey/package.json pnpm*.yaml ./
COPY --from=fetch /calckey/packages/backend/package.json packages/backend/package.json
COPY --from=fetch /calckey/packages/client/package.json packages/client/package.json
COPY --from=fetch /calckey/packages/sw/package.json packages/sw/package.json
COPY --from=fetch /calckey/packages/calckey-js/package.json packages/calckey-js/package.json
COPY --from=fetch /calckey/packages/megalodon/package.json packages/megalodon/package.json
COPY --from=fetch /calckey/packages/backend/native-utils/package.json packages/backend/native-utils/package.json
COPY --from=fetch /calckey/packages/backend/native-utils/npm/linux-x64-musl/package.json packages/backend/native-utils/npm/linux-x64-musl/package.json
COPY --from=fetch /calckey/packages/backend/native-utils/npm/linux-arm64-musl/package.json packages/backend/native-utils/npm/linux-arm64-musl/package.json

# Configure corepack and pnpm, and install dev mode dependencies for compilation
RUN tree && corepack enable && corepack prepare pnpm@latest --activate && pnpm i --frozen-lockfile

# Copy in the rest of the native-utils rust files
COPY --from=fetch /calckey/packages/backend/native-utils packages/backend/native-utils/

# Compile native-utils
RUN pnpm run --filter native-utils build

# Copy in the rest of the files to compile
COPY --from=fetch /calckey ./
RUN env NODE_ENV=production sh -c "pnpm run --filter '!native-utils' build && pnpm run gulp"

# Trim down the dependencies to only those for production
RUN pnpm i --prod --frozen-lockfile


## Runtime container
FROM alpine:3.18
WORKDIR /calckey

# Install runtime dependencies
RUN apk add --no-cache --no-progress tini ffmpeg vips-dev zip unzip nodejs-current

# Get Calckey
COPY --from=fetch /calckey ./

COPY --from=build /calckey/packages/megalodon /calckey/packages/megalodon

# Copy node modules
COPY --from=build /calckey/node_modules /calckey/node_modules
COPY --from=build /calckey/packages/backend/node_modules /calckey/packages/backend/node_modules
COPY --from=build /calckey/packages/sw/node_modules /calckey/packages/sw/node_modules
COPY --from=build /calckey/packages/client/node_modules /calckey/packages/client/node_modules
COPY --from=build /calckey/packages/calckey-js/node_modules /calckey/packages/calckey-js/node_modules

# Copy the finished compiled files
COPY --from=build /calckey/built /calckey/built
COPY --from=build /calckey/packages/backend/built /calckey/packages/backend/built
COPY --from=build /calckey/packages/backend/assets/instance.css /calckey/packages/backend/assets/instance.css
COPY --from=build /calckey/packages/backend/native-utils/built /calckey/packages/backend/native-utils/built

RUN corepack enable && corepack prepare pnpm@latest --activate
ENV NODE_ENV=production
VOLUME "/calckey/files"
ENTRYPOINT [ "/sbin/tini", "--" ]
CMD [ "pnpm", "run", "migrateandstart" ]
