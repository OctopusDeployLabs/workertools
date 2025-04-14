ARG BASE_IMAGE
FROM --platform=linux/amd64 ${BASE_IMAGE}:latest

# Get Terraform
# https://developer.hashicorp.com/terraform/downloads
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list && \
    apt update && apt install -y terraform

# Get Node.js
# https://nodejs.org/en/download/package-manager/all
RUN curl -fsSL https://deb.nodesource.com/setup_23.x -o nodesource_setup.sh && \
    bash nodesource_setup.sh && \
    apt-get install -y nodejs && \
    rm nodesource_setup.sh

# Get CDK
# https://docs.aws.amazon.com/cdk/v2/guide/getting_started.html
RUN npm install -g aws-cdk

# Get AWS CLI
# https://docs.aws.amazon.com/cli/latest/userguide/install-linux.html#install-linux-awscli
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm awscliv2.zip && \
    rm -rf ./aws

# Get ECS CLI
# https://github.com/aws/amazon-ecs-cli
RUN curl --silent --location "https://amazon-ecs-cli.s3.amazonaws.com/ecs-cli-linux-amd64-latest" -o /usr/local/bin/ecs-cli && \
    chmod +x /usr/local/bin/ecs-cli

# GET eksctl
# https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html
RUN curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp && \
    mv /tmp/eksctl /usr/local/bin

RUN pwsh -c 'Install-Module -Force -Name AWS.Tools.Installer -AllowClobber -Scope AllUsers'

RUN pwsh -c 'Install-Module -Force -Name AWS.Tools.Common -AllowClobber -Scope AllUsers'