FROM bitnami/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/GregoryAM-SP/The-Minecraft-Overviewer.git .

FROM ubuntu:jammy
WORKDIR /app
RUN apt-get update && apt-get install --no-install-recommends -y build-essential gcc python3 python3-dev python3-pil python3-numpy && apt-get clean && rm -rf /var/lib/apt/lists/*
COPY --from=git_clone /git_clone/ .
RUN python3 setup.py build

ENTRYPOINT [ "python", "overviewer.py" ]