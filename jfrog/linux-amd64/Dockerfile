ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest

ARG DEBIAN_FRONTEND noninteractive
ARG JFROG_CLI_VERSION=2.78.3

# Update the package list and install
RUN curl -fL https://install-cli.jfrog.io | sh -s ${JFROG_CLI_VERSION}