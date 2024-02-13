FROM --platform=linux/arm64 mcr.microsoft.com/dotnet/runtime-deps:8.0 AS base

ARG TARGETOS
ARG TARGETARCH
ARG PS_MAJOR_VERSION
ARG PS_VERSION

# Get pre-req tooling
RUN apt-get update && \
    apt-get install -y libc6 wget unzip apt-utils curl apt-transport-https software-properties-common jq

# Get yq, yaml parser
RUN wget -qO /usr/local/bin/yq https://github.com/mikefarah/yq/releases/latest/download/yq_linux_arm64 && \
    chmod a+x /usr/local/bin/yq

# Download the powershell '.tar.gz' archive
RUN curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v${PS_VERSION}/powershell-${PS_VERSION}-${TARGETOS}-${TARGETARCH}.tar.gz

# Create the target folder where powershell will be placed
RUN mkdir -p /opt/microsoft/powershell/${PS_MAJOR_VERSION}

# Expand powershell to the target folder
RUN tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/${PS_MAJOR_VERSION}

# Set execute permissions
RUN chmod +x /opt/microsoft/powershell/${PS_MAJOR_VERSION}/pwsh

# Create the symbolic link that points to pwsh
RUN ln -s /opt/microsoft/powershell/${PS_MAJOR_VERSION}/pwsh /usr/bin/pwsh

# We know this won't reduce the image size at all. It's just to make the filesystem a little tidier.
RUN rm -rf /tmp/*

# Get python & groff to support Python scripts in execution container
RUN apt-get install -y python3-pip groff

# Install the Octopus CLI
RUN curl -L https://github.com/OctopusDeploy/cli/raw/main/scripts/install.sh | bash
