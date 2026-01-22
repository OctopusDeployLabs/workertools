FROM mcr.microsoft.com/dotnet/runtime-deps:8.0 AS base

ARG DEBIAN_FRONTEND noninteractive
ARG VERSION 3.7.8

# Get pre-req tooling
RUN apt-get update && \
    apt-get install -y wget unzip curl jq

# Get yq, yaml parser
RUN wget -qO /usr/local/bin/yq https://github.com/mikefarah/yq/releases/latest/download/yq_linux_${TARGETARCH} && \
    chmod a+x /usr/local/bin/yq

# Install Argo Worfklows CLI
RUN curl -sSL -o argo-linux-${TARGETARCH}.gz https://github.com/argoproj/argo-workflows/releases/download/v$VERSION/argo-linux-${TARGETARCH}.gz \
    && gunzip argo-linux-${TARGETARCH}.gz \
    && install -m 555 argo-linux-${TARGETARCH} /usr/local/bin/argo \
    && rm argo-linux-${TARGETARCH}


# We know this won't reduce the image size at all. It's just to make the filesystem a little tidier.
RUN rm -rf /tmp/*

