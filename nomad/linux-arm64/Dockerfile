ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest

ARG DEBIAN_FRONTEND noninteractive
ARG NOMAD_VERSION=1.9.5
ARG NOMAD_PACKAGE=nomad

RUN apt update && apt install -y gpg wget coreutils

# Get Nomad - https://developer.hashicorp.com/nomad/docs/install
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list && \
    apt update && apt install -y ${NOMAD_PACKAGE}=${NOMAD_VERSION}-1