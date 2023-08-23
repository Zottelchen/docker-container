FROM bitnami/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/GregoryAM-SP/The-Minecraft-Overviewer.git .

FROM ubuntu:jammy
WORKDIR /app
RUN apt-get update && apt-get install --no-install-recommends -y wget ca-certificates build-essential gcc python3 python3-dev python3-pil python3-numpy && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN adduser nonroot && addgroup nonroot nonroot
USER nonroot
RUN mkdir -p ~/.minecraft/versions/1.20/ && wget https://overviewer.org/textures/1.20 -O ~/.minecraft/versions/1.20/1.20.jar && \
    mkdir -p ~/.minecraft/versions/1.17/ && wget https://overviewer.org/textures/1.17 -O ~/.minecraft/versions/1.17/1.17.jar
COPY --from=git_clone --chown=nonroot:nonroot /git_clone/ .
RUN python3 setup.py build



ENTRYPOINT [ "python3", "overviewer.py" ]