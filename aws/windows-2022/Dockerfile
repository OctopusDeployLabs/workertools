# escape=`
ARG BASE_IMAGE
FROM --platform=windows/amd64 ${BASE_IMAGE}:latest
SHELL ["powershell", "-Command"]

# Install Terraform
RUN choco install terraform -y --no-progress

# Install AWS CLI
RUN choco install awscli -y --no-progress

# Install ECS CLI
RUN choco install ecs-cli -y --no-progress; `
    Import-Module $env:ChocolateyInstall\helpers\chocolateyProfile.psm1; `
    refreshenv

# Install eksctl
RUN choco install eksctl -y --no-progress; `
    Import-Module $env:ChocolateyInstall\helpers\chocolateyProfile.psm1; `
    refreshenv

RUN Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force; `
    Install-Module -name AWSPowerShell.NetCore -Force