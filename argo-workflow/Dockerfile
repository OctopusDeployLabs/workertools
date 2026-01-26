FROM mcr.microsoft.com/dotnet/runtime-deps:8.0 AS base

ARG DEBIAN_FRONTEND=noninteractive
ARG KUBECTL_MAJOR_MINOR_VERSION=1.30
ARG ARGO_WORKFLOW_VERSION=3.7.8
ARG YQ_VERSION=4.49.2
ARG TARGETARCH 

# Get pre-req tooling
# xxd is required to use octopus_parameters
RUN apt-get update && \
    apt-get install -y wget unzip curl jq xxd

# install packages required to install kubectl
RUN apt-get install -y apt-transport-https ca-certificates  gnupg

# Get yq, yaml parser
RUN wget -qO /usr/local/bin/yq https://github.com/mikefarah/yq/releases/download/v${YQ_VERSION}/yq_linux_${TARGETARCH} && \
    chmod a+x /usr/local/bin/yq

# Get kubectl
# https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-native-package-management
RUN mkdir -m 755 -p /etc/apt/keyrings && \
    curl -fsSL "https://pkgs.k8s.io/core:/stable:/v${KUBECTL_MAJOR_MINOR_VERSION}/deb/Release.key" | gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg && \
    echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v${KUBECTL_MAJOR_MINOR_VERSION}/deb/ /" | tee /etc/apt/sources.list.d/kubernetes.list && \
    apt-get update && apt-get install -y kubectl


# Install Argo Workflows CLI
RUN curl -sLO  https://github.com/argoproj/argo-workflows/releases/download/v$ARGO_WORKFLOW_VERSION/argo-linux-${TARGETARCH}.gz \
    && gunzip argo-linux-${TARGETARCH}.gz \
    && install -m 555 argo-linux-${TARGETARCH} /usr/local/bin/argo \
    && rm argo-linux-${TARGETARCH}


# We know this won't reduce the image size at all. It's just to make the filesystem a little tidier.
RUN rm -rf /tmp/*

