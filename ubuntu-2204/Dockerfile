FROM ubuntu:22.04

# get `wget` & software-properties-common
# https://learn.microsoft.com/en-us/powershell/scripting/install/install-ubuntu?view=powershell-7.3#installation-via-package-repository
RUN apt-get update && \
    apt-get install -y wget unzip apt-utils curl apt-transport-https software-properties-common

# get powershell for 22.04 to support PowerShell scripts in execution container
RUN wget -q https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    apt-get update && \
    apt-get install -y powershell

# Get python & groff to support Python scripts in execution container
RUN apt-get install -y python3-pip groff

# Install the Octopus CLI
RUN apt update && apt install --no-install-recommends gnupg curl ca-certificates apt-transport-https -y && \
    curl -sSfL https://apt.octopus.com/public.key | apt-key add - && \
    sh -c "echo deb https://apt.octopus.com/ stable main > /etc/apt/sources.list.d/octopus.com.list" && \
    apt update && apt install octopuscli -y