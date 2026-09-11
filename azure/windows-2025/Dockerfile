# escape=`
ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest
SHELL ["powershell", "-Command"]

# Install Terraform
RUN choco install terraform -y --no-progress

# Install Azure CLI
RUN choco install azure-cli -y --no-progress

# Install Azcopy
RUN choco install azcopy10 -y --no-progress

RUN Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force; `
    Install-Module -Force -Name Az -AllowClobber -Scope AllUsers

