ARG BASE_IMAGE
FROM --platform=linux/arm64 ${BASE_IMAGE}:latest

ARG DEBIAN_FRONTEND noninteractive
ARG KUBECTL_MAJOR_MINOR_VERSION=1.30

# Get kubectl
# https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-native-package-management
RUN mkdir -m 755 -p /etc/apt/keyrings && \
    curl -fsSL "https://pkgs.k8s.io/core:/stable:/v${KUBECTL_MAJOR_MINOR_VERSION}/deb/Release.key" | gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg && \
    echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v${KUBECTL_MAJOR_MINOR_VERSION}/deb/ /" | tee /etc/apt/sources.list.d/kubernetes.list && \
    apt-get update && apt-get install -y kubectl

# Install Argo CD
RUN curl -sSL -o argocd-linux-arm64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-arm64 && \
    install -m 555 argocd-linux-arm64 /usr/local/bin/argocd && \
    rm argocd-linux-arm64

# Get latest Helm v3
RUN wget --quiet -O - https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# JQ
RUN apt-get install -y jq
