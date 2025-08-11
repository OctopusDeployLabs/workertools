# escape=`
ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest
SHELL ["powershell", "-Command"]

ARG JFROG_CLI_VERSION=2.78.3
ENV JFROG_CLI_VERSION=${JFROG_CLI_VERSION}
ENV JFROG_HOME="C:\\jfrog-cli"

# Download JFrog CLI to the install location
RUN New-Item -ItemType Directory -Path $env:JFROG_HOME | Out-Null ; `
    Invoke-WebRequest -Uri "https://releases.jfrog.io/artifactory/jfrog-cli/v2-jf/${env:JFROG_CLI_VERSION}/jfrog-cli-windows-amd64/jf.exe" -OutFile "$env:JFROG_HOME\\jf.exe"

# Update PATH environment variable using Docker ENV
ENV PATH="${JFROG_HOME};${PATH}"
