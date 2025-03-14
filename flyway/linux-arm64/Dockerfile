ARG BASE_IMAGE
FROM --platform=linux/arm64 ${BASE_IMAGE}:latest

ARG FLYWAY_VERSION=10.7.1

# Get JRE
RUN apt-get update && apt-get install -y openjdk-17-jre-headless

# Get SQL Fluff for Flyway Check Command
# Added --break-system-packages as a result of https://peps.python.org/pep-0668/
# Setting a virtual env in a container isnt needed.
RUN pip3 install sqlfluff==1.2.1 --break-system-packages

# Install AWS CLI to support IAM role authentication
RUN apt-get update && apt-get install unzip \
  && curl "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip" \
  && unzip awscliv2.zip \
  && rm awscliv2.zip \
  && ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update 

# Change the workdir to flyway to install flyway binaries
WORKDIR /flyway

# Install flyway
RUN curl -L https://download.red-gate.com/maven/release/com/redgate/flyway/flyway-commandline/${FLYWAY_VERSION}/flyway-commandline-${FLYWAY_VERSION}.tar.gz -o flyway-commandline-${FLYWAY_VERSION}.tar.gz \
  && tar -xzf flyway-commandline-${FLYWAY_VERSION}.tar.gz --strip-components=1 \
  && rm flyway-commandline-${FLYWAY_VERSION}.tar.gz \
  # Make the /flyway/flyway command an executable
  && chmod +x /flyway/flyway \
  # Make it so any user can call /flyway/flyway 
  && ln -s /flyway/flyway /usr/local/bin/flyway

# Octopus expects to start in the default directory
WORKDIR /