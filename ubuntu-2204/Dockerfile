FROM ubuntu:22.04

# Get pre-req tooling
RUN apt-get update && \
    apt-get install -y wget unzip apt-utils curl apt-transport-https software-properties-common

# get powershell for 22.04 to support PowerShell scripts in execution container
# https://learn.microsoft.com/en-us/powershell/scripting/install/install-ubuntu?view=powershell-7.3#installation-via-package-repository
RUN wget -q https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    apt-get update && \
    apt-get install -y powershell

# Get python & groff to support Python scripts in execution container
RUN apt-get install -y python3-pip groff

# Install the legacy Octopus CLI
RUN apt update && apt install --no-install-recommends gnupg curl ca-certificates apt-transport-https -y && \
    wget -O- https://apt.octopus.com/public.key | gpg --dearmor | tee /usr/share/keyrings/octopus-cli-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/octopus-cli-keyring.gpg] https://apt.octopus.com/ stable main" | tee /etc/apt/sources.list.d/octopus.com.list && \
    apt update && apt install -y octopuscli

# Install vNext Octopus CLI
RUN apt install -y octopus-cli