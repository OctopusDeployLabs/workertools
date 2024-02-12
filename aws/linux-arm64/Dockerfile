ARG BASE_IMAGE
FROM --platform=linux/arm64 ${BASE_IMAGE}:latest

# Get Terraform
# https://developer.hashicorp.com/terraform/downloads
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list && \
    apt update && apt install -y terraform

# Get AWS CLI
# https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
RUN curl --silent -L "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm -f awscliv2.zip

# Get ECS CLI
# https://github.com/aws/amazon-ecs-cli
RUN curl --silent --location "https://amazon-ecs-cli.s3.amazonaws.com/ecs-cli-linux-arm64-latest" -o /usr/local/bin/ecs-cli && \
    chmod +x /usr/local/bin/ecs-cli

# Get EKS CLI
# https://github.com/weaveworks/eksctl
RUN curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_arm64.tar.gz" | tar xz -C /tmp && \
    mv /tmp/eksctl /usr/local/bin

# AWS Powershell tools
# Can't be installed on ARM currently due to this issue: https://github.com/docker/buildx/issues/1422
# tl;dr - qemu emulation of arm64 when run on ubuntu 22.04 doesnt allow for the install.
# An error of: "5.066 Illegal instruction (core dumped)" is returned

#RUN pwsh -c 'Install-Module -Force -Name AWS.Tools.Installer -AllowClobber -Scope AllUsers'
#RUN pwsh -c 'Install-Module -Force -Name AWS.Tools.Common -AllowClobber -Scope AllUsers'