ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest

ARG DEBIAN_FRONTEND noninteractive
ARG BWS_VERSION="1.0.0"
ARG BWS_FILENAME="bws-x86_64-unknown-linux-gnu-${BWS_VERSION}.zip"
ARG BWS_URL="https://github.com/bitwarden/sdk-sm/releases/download/bws-v${BWS_VERSION}/${BWS_FILENAME}"

RUN curl -L -o /tmp/bws.zip ${BWS_URL} && \
    unzip /tmp/bws.zip -d /usr/local/bin/

