ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest

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
RUN pwsh -c 'Install-Module -Name Az -Repository PSGallery -Scope AllUsers -AllowClobber -Force'

# Get AZCopy
# https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-install-linux-package?tabs=apt
RUN set -eux; \
    curl -sSL "https://aka.ms/downloadazcopy-v10-linux" -o azcopy.tar.gz; \
    tar -xzf azcopy.tar.gz; \
    mv azcopy_linux_*/azcopy /usr/local/bin/; \
    chmod +x /usr/local/bin/azcopy; \
    rm -rf azcopy_linux_* azcopy.tar.gz