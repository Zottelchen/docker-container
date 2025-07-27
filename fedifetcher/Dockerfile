FROM cgr.dev/chainguard/git:latest AS git_clone
WORKDIR /git_clone
RUN git clone --depth=1 https://github.com/nanos/FediFetcher.git .

FROM gcr.io/distroless/python3-debian12:latest AS builder
WORKDIR /app
COPY --from=git_clone /git_clone/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt --user --upgrade && mkdir -p /app/artifacts/ && chown nonroot:nonroot -R /app/artifacts/

FROM gcr.io/distroless/python3-debian12:latest
WORKDIR /app
# Make sure you update Python version in path
COPY --from=builder /home/nonroot/.local/lib/python3.12/site-packages /home/nonroot/.local/lib/python3.12/site-packages
COPY --from=builder --chown=nonroot:nonroot /app/artifacts/. /app/artifacts/
COPY --from=git_clone --chown=nonroot:nonroot /git_clone/find_posts.py /app/

ENV PYTHONUNBUFFERED=1
ENTRYPOINT [ "python", "/app/find_posts.py" ]
