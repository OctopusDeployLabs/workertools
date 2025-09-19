ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest

ARG DEBIAN_FRONTEND noninteractive
ARG TRIVY_VERSION=0.66.0

RUN apt-get update && \
    apt-get install -y wget apt-transport-https gnupg lsb-release && \
    wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | apt-key add - && \
    echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main > /etc/apt/sources.list.d/trivy.list && \
    apt-get update && \
    apt-get install -y trivy=${TRIVY_VERSION} && \
    rm -rf /var/lib/apt/lists/*
