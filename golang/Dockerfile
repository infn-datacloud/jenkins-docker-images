FROM ubuntu:20.04

# Install patch command
RUN apt-get update && apt-get install -y --no-install-recommends \
    make patch ca-certificates wget git \
  && rm -rf /var/lib/apt/lists/*
RUN wget --no-check-certificate https://go.dev/dl/go1.21.0.linux-amd64.tar.gz && \
    tar -xvf go1.21.0.linux-amd64.tar.gz && \
    mv go /usr/local/ && \
    rm go1.21.0.linux-amd64.tar.gz

ENV GOROOT="/usr/local/go"
ENV GOPATH="${HOME}/go"
ENV PATH="${PATH}:$GOROOT/bin"
