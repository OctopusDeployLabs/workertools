ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest

ARG DEBIAN_FRONTEND noninteractive

# Install GitHub CLI
RUN mkdir -p -m 755 /etc/apt/keyrings \
    && wget -qO- https://cli.github.com/packages/githubcli-archive-keyring.gpg | tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
    && chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
    && apt update \
    && apt install gh -y

# Get AWS CLI
# https://docs.aws.amazon.com/cli/latest/userguide/install-linux.html#install-linux-awscli
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm awscliv2.zip && \
    rm -rf ./aws

# AWS Powershell tools
RUN pwsh -c 'Install-Module -Force -Name AWS.Tools.Installer -AllowClobber -Scope AllUsers'
RUN pwsh -c 'Install-Module -Force -Name AWS.Tools.Common -AllowClobber -Scope AllUsers'

# Get Azure CLI
# https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Get AZ Powershell core modules
# https://learn.microsoft.com/en-us/powershell/azure/install-azure-powershell?view=azps-11.2.0
RUN pwsh -c 'Install-Module -Name Az -Repository PSGallery -Scope AllUsers -AllowClobber -Force'

# Install Google Cloud CLI
# https://cloud.google.com/sdk/docs/downloads-apt-get
RUN apt-get install -y ca-certificates gnupg && \
    curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    apt-get update && apt-get install -y google-cloud-sdk