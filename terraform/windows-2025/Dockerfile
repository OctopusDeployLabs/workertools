# escape=`
ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest
LABEL org.opencontainers.image.source="https://github.com/OctopusDeployLabs/workertools"
SHELL ["powershell", "-Command"]

# Install Terraform
RUN choco install terraform -y --no-progress