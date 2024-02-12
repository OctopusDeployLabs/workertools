# escape=`
ARG BASE_IMAGE
FROM --platform=windows/amd64 ${BASE_IMAGE}:latest
SHELL ["powershell", "-Command"]

# Install Terraform
RUN choco install git -y --no-progress

# Install Terraform
RUN choco install terraform -y --no-progress