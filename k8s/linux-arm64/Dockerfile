ARG BASE_IMAGE
FROM --platform=linux/arm64 ${BASE_IMAGE}:latest

ARG DEBIAN_FRONTEND noninteractive
ARG KUBECTL_MAJOR_MINOR_VERSION=1.29
ARG GOOGLE_CLOUD_CLI_VERSION=462.0.0-0

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

# Get Kubelogin
RUN wget --quiet https://github.com/Azure/kubelogin/releases/latest/download/kubelogin-linux-arm64.zip && \
    unzip kubelogin-linux-arm64.zip -d kubelogin-linux-arm64 && \
    mv kubelogin-linux-arm64/bin/linux_arm64/kubelogin /usr/local/bin && \
    rm -rf kubelogin-linux-arm64 && \
    rm kubelogin-linux-arm64.zip
    
# Get EKS CLI
# https://github.com/weaveworks/eksctl
RUN curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_arm64.tar.gz" | tar xz -C /tmp && \
    mv /tmp/eksctl /usr/local/bin

# Get aws-cli
# https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
RUN curl --silent -L "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm -f awscliv2.zip

# Get gke-gcloud-auth-plugin (reqd for kubectl 1.26+)
# See https://github.com/OctopusDeploy/Issues/issues/7621 for more info
RUN curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    apt-get update && apt-get install -y google-cloud-sdk-gke-gcloud-auth-plugin

# Get the Istio CLI
# https://istio.io/docs/ops/diagnostic-tools/istioctl/
RUN curl -sL https://istio.io/downloadIstioctl | sh - && \
    mv /root/.istioctl/bin/istioctl /usr/local/bin/istioctl && \
    rm -rf /root/.istioctl

# Get the Linkerd CLI
# https://linkerd.io/2/getting-started/
RUN curl -sL https://run.linkerd.io/install | sh && \
    cp /root/.linkerd2/bin/linkerd /usr/local/bin && \
    rm -rf /root/.linkerd2

# Skopeo
# https://github.com/containers/skopeo/blob/main/install.md#debian
RUN apt-get update && apt-get install -y skopeo

# Get Azure CLI
# https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Install Google Cloud CLI
# https://cloud.google.com/sdk/docs/downloads-apt-get
RUN apt-get install -y ca-certificates gnupg && \
    curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    apt-get update && apt-get install -y google-cloud-sdk=${GOOGLE_CLOUD_CLI_VERSION}

# JQ
RUN apt-get install -y jq

# AZ Powershell Modules
# Can't be installed on ARM currently due to this issue: https://github.com/docker/buildx/issues/1422
# tl;dr - qemu emulation of arm64 when run on ubuntu 22.04 doesnt allow for the install.
# An error of: "5.066 Illegal instruction (core dumped)" is returned

# One-liner install
# RUN pwsh -c 'Install-Module -Name Az -Repository PSGallery -Scope AllUsers -AllowClobber -Force'

# Alternative install
# RUN azps_download_url=$(curl -s "https://api.github.com/repos/azure/azure-powershell/releases/latest" | jq -r '.assets[] | select(.content_type == "application/x-gzip" and (.name | endswith(".tar.gz"))) | .browser_download_url ') && \
#     curl -L -o /tmp/azure-powershell.tar.gz $azps_download_url && \
#     mkdir /tmp/latest && \
#     tar -zxvf /tmp/azure-powershell.tar.gz -C /tmp/latest && \
#     pwsh -Command /tmp/latest/InstallModule.ps1 -Scope AllUsers ;