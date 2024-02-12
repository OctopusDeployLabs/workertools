FROM --platform=linux/amd64 mcr.microsoft.com/dotnet/runtime-deps:6.0 AS base

ARG PS_VERSION

# Get pre-req tooling
RUN apt-get update && \
    apt-get install -y libc6 wget unzip apt-utils curl apt-transport-https software-properties-common jq

# Get yq, yaml parser
RUN wget -qO /usr/local/bin/yq https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 && \
    chmod a+x /usr/local/bin/yq

# Download the PowerShell package file
RUN wget https://github.com/PowerShell/PowerShell/releases/download/v${PS_VERSION}/powershell_${PS_VERSION}-1.deb_amd64.deb

###################################
# Install the PowerShell package
RUN dpkg -i powershell_${PS_VERSION}-1.deb_amd64.deb

# Resolve missing dependencies and finish the install (if necessary)
RUN apt-get install -f

# Delete the downloaded package file
RUN rm powershell_${PS_VERSION}-1.deb_amd64.deb

# Get python & groff to support Python scripts in execution container
RUN apt-get install -y python3-pip groff

# Install the Octopus CLI
RUN curl -L https://github.com/OctopusDeploy/cli/raw/main/scripts/install.sh | bash

# We know this won't reduce the image size at all. It's just to make the filesystem a little tidier.
RUN rm -rf /tmp/*
