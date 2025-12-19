FROM cgr.dev/chainguard/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/GregoryAM-SP/The-Minecraft-Overviewer.git .

FROM ubuntu:22.04
RUN apt-get update && apt-get install --no-install-recommends -y wget ca-certificates build-essential gcc python3 python3-dev python3-pil python3-numpy && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN adduser nonroot && addgroup nonroot nonroot
USER nonroot
WORKDIR /app
RUN mkdir -p ~/.minecraft/versions/1.20/ && wget --progress=dot:giga https://piston-data.mojang.com/v1/objects/05b6f1c6b46a29d6ea82b4e0d42190e42402030f/client.jar -O ~/.minecraft/versions/1.20/1.20.jar && \
    mkdir -p ~/.minecraft/versions/1.17/ && wget --progress=dot:giga https://piston-data.mojang.com/v1/objects/8d9b65467c7913fcf6f5b2e729d44a1e00fde150/client.jar -O ~/.minecraft/versions/1.17/1.17.jar
COPY --from=git_clone --chown=nonroot:nonroot /git_clone/ .
RUN python3 setup.py build

ENV PYTHONUNBUFFERED=1
ENTRYPOINT [ "python3", "overviewer.py" ]