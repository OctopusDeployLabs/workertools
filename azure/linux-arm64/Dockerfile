ARG BASE_IMAGE
FROM --platform=linux/arm64 ${BASE_IMAGE}:latest

ARG DEBIAN_FRONTEND noninteractive

# Get Terraform
# https://developer.hashicorp.com/terraform/downloads
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list && \
    apt update && apt install -y terraform

# Get Azure CLI
# https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Get AZ Powershell core modules
# https://learn.microsoft.com/en-us/powershell/azure/install-azure-powershell?view=azps-11.2.0

# Can't be installed on ARM currently due to this issue: https://github.com/docker/buildx/issues/1422
# tl;dr - qemu emulation of arm64 when run on ubuntu 22.04 doesnt allow for the install.
# An error of: "5.066 Illegal instruction (core dumped)" is returned

# One-liner install
# RUN pwsh -c 'Install-Module -Name Az -Repository PSGallery -Scope AllUsers -AllowClobber -Force'