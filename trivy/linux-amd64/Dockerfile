ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest

ARG DEBIAN_FRONTEND noninteractive
ARG TRIVY_VERSION=0.64.0

RUN curl -L https://github.com/aquasecurity/trivy/releases/download/v${TRIVY_VERSION}/trivy_${TRIVY_VERSION}_Linux-64bit.tar.gz -o trivy-${TRIVY_VERSION}.tar.gz \
  && tar -xzf trivy-${TRIVY_VERSION}.tar.gz --strip-components=1 \
  && rm trivy-${TRIVY_VERSION}.tar.gz \
  # Make the /trivy/trivy command an executable
  && chmod +x /trivy/trivy \
  # Make it so any user can call /trivy/trivy
  && ln -s /trivy/trivy /usr/local/bin/trivy
