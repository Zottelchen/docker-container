FROM bitnami/git:latest as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/GregoryAM-SP/The-Minecraft-Overviewer.git .

FROM python:3.8
WORKDIR /app
RUN python3 setup.py build

ENTRYPOINT [ "python", "overviewer.py" ]