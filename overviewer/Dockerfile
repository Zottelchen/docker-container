FROM cgr.dev/chainguard/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/overviewer/Minecraft-Overviewer.git .

FROM ubuntu:24.04

# Install runtime and build deps, then clean
RUN apt-get update \
 && apt-get install --no-install-recommends -y \
      wget ca-certificates \
      build-essential gcc \
      python3 python3-dev python3-pil python3-numpy \
 && rm -rf /var/lib/apt/lists/*

# Create non-root user and home dir explicitly
RUN useradd -m -d /home/nonroot -s /bin/bash nonroot

USER nonroot
WORKDIR /app

# Make sure HOME is set correctly for nonroot
ENV HOME=/home/nonroot

# Download Minecraft client jars into user's home
RUN mkdir -p "$HOME/.minecraft/versions/1.20" "$HOME/.minecraft/versions/1.17" && \
    wget --progress=dot:giga \
      https://piston-data.mojang.com/v1/objects/05b6f1c6b46a29d6ea82b4e0d42190e42402030f/client.jar \
      -O "$HOME/.minecraft/versions/1.20/1.20.jar" && \
    wget --progress=dot:giga \
      https://piston-data.mojang.com/v1/objects/8d9b65467c7913fcf6f5b2e729d44a1e00fde150/client.jar \
      -O "$HOME/.minecraft/versions/1.17/1.17.jar"

# Copy source and ensure ownership
COPY --from=git_clone --chown=nonroot:nonroot /git_clone/ /app/

# Build Overviewer as non-root
RUN python3 setup.py build

ENV PYTHONUNBUFFERED=1

ENTRYPOINT ["python3", "overviewer.py"]
