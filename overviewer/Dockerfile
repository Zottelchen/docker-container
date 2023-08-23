FROM bitnami/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/GregoryAM-SP/The-Minecraft-Overviewer.git .

FROM python:3.8
WORKDIR /app
RUN apt-get update && apt-get install --no-install-recommends -y build-essential gcc && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN pip3 install numpy pillow
COPY --from=git_clone /git_clone/ .
RUN python3 setup.py build

ENTRYPOINT [ "python", "overviewer.py" ]