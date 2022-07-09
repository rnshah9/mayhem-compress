# Build Stage
FROM --platform=linux/amd64 ubuntu:20.04 as builder

## Install build dependencies.
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y git wget tar 

RUN wget https://go.dev/dl/go1.18.1.linux-amd64.tar.gz
RUN tar -C /usr/local -xvf go1.18.1.linux-amd64.tar.gz
ENV PATH=$PATH:/usr/local/go/bin

RUN go install github.com/goreleaser/goreleaser@latest
ENV PATH=$PATH:/root/go/bin

ADD . /mayhem-compress
WORKDIR /mayhem-compress

RUN goreleaser build --skip-validate --single-target --snapshot

FROM --platform=linux/amd64 ubuntu:20.04

COPY --from=builder /mayhem-compress/dist/s2c_linux_amd64_v1/s2c /

