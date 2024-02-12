ARG BASE_IMAGE
FROM --platform=linux/arm64 ${BASE_IMAGE}:latest

ARG LIQUIBASE_VERSION=4.26.0

# Download and install AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip" \
  && unzip awscliv2.zip \
  && rm awscliv2.zip \
  && ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update

# Install Java
RUN apt-get update && apt-get install openjdk-17-jdk -y

# Download and install Liquibase
RUN curl -L https://github.com/liquibase/liquibase/releases/download/v${LIQUIBASE_VERSION}/liquibase-${LIQUIBASE_VERSION}.zip -o liquibase.zip \
  && unzip liquibase.zip \
  && rm liquibase.zip

# Set environment variable to determine if in container
ENV IsContainer=true