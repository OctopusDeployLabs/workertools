ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest

ARG DEBIAN_FRONTEND noninteractive
ARG VAULT_VERSION=1.15.5

RUN apt update && apt install -y gpg wget libcap2-bin

# Get Vault
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list && \
    apt update && apt install -y vault=${VAULT_VERSION}-1

# Add CAP_IPC_LOCK capabilities. https://www.vaultproject.io/docs/configuration
RUN setcap -r /usr/bin/vault
