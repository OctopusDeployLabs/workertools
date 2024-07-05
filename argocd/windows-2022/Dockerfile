# escape=`
ARG BASE_IMAGE
FROM --platform=windows/amd64 ${BASE_IMAGE}:latest
SHELL ["powershell", "-Command"]

RUN choco install kubernetes-cli -y --no-progress
RUN choco install -y kubernetes-helm --no-progress
RUN choco install argocd-cli -y --no-progress
