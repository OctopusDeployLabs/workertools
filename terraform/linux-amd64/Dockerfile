ARG BASE_IMAGE
FROM --platform=linux/amd64 ${BASE_IMAGE}:latest

ARG DEBIAN_FRONTEND noninteractive
ARG TERRAFORM_VERSION=1.7.2

# Install git
RUN apt-get update && apt-get install -y git 

# Get Terraform
# https://developer.hashicorp.com/terraform/downloads
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list && \
    apt update && apt install -y terraform=${TERRAFORM_VERSION}-1