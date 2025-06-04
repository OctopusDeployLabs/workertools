# escape=`
ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest
SHELL ["powershell", "-Command"]

# Install Terraform
RUN choco install git -y --no-progress

# Install Terraform
RUN choco install terraform -y --no-progress