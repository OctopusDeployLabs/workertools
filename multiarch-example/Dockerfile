FROM --platform=$TARGETPLATFORM mcr.microsoft.com/dotnet/runtime-deps:6.0 AS base

ARG TARGETOS
ARG TARGETARCH

# Get pre-req tooling
RUN apt-get update && \
    apt-get install -y libc6 wget unzip apt-utils curl apt-transport-https software-properties-common

FROM base As build-ps-arm64
ARG PS_MAJOR_VERSION
ARG PS_VERSION

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

FROM base As build-ps-amd64
ARG PS_VERSION

# Download the PowerShell package file
RUN wget https://github.com/PowerShell/PowerShell/releases/download/v${PS_VERSION}/powershell_${PS_VERSION}-1.deb_amd64.deb

###################################
# Install the PowerShell package
RUN dpkg -i powershell_${PS_VERSION}-1.deb_amd64.deb

# Resolve missing dependencies and finish the install (if necessary)
RUN apt-get install -f

# Delete the downloaded package file
RUN rm powershell_${PS_VERSION}-1.deb_amd64.deb

FROM build-ps-${TARGETARCH} as final

# Get python & groff to support Python scripts in execution container
RUN apt-get install -y python3-pip groff

# Install the Octopus CLI
RUN curl -L https://github.com/OctopusDeploy/cli/raw/main/scripts/install.sh | bash
