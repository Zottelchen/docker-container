FROM bitnami/git as git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/nanos/FediFetcher.git .


FROM cgr.dev/chainguard/python:latest-dev as builder
WORKDIR /app
COPY --from=git_clone /git_clone/requirements.txt .
RUN pip install -r requirements.txt --user --upgrade

FROM cgr.dev/chainguard/python:latest
WORKDIR /app
# Make sure you update Python version in path
COPY --from=builder /home/nonroot/.local/lib/python3.11/site-packages /home/nonroot/.local/lib/python3.11/site-packages
RUN mkdir -p /app/artifacts/
COPY --from=git_clone /git_clone/find_posts.py /app/
ENTRYPOINT [ "python", "/app/find_posts.py" ]