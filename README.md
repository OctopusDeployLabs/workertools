# Overview

This repository contains Dockerfiles used to build container images for common tools used with the [execution container](https://octopus.com/docs/projects/steps/execution-containers-for-workers) feature of Octopus Deploy.

**Please consider this repository and any container images provided as-is. If there are any issues please do not contact the Octopus support team.**

## Platforms

Images are typically available for:

- `linux/amd64`
- `linux/arm64` 
- `windows/amd64` (Windows 2022)

> Some tools may not provide `linux/arm64` or `windows/amd64` platform support.

## Available images

The following images are built from this repository:

- [Base workertools](#base-workertools) (`octopuslabs/workertools`)
- [AWS workertools](#aws-workertools) (`octopuslabs/aws-workertools`)
- [Azure workertools](#azure-workertools) (`octopuslabs/azure-workertools`)
- [Flyway workertools](#flyway-workertools) (`octopuslabs/flyway-workertools`)
- [GCP workertools](#gcp-workertools) (`octopuslabs/gcp-workertools`)
- [Kubernetes workertools](#kubernetes-workertools) (`octopuslabs/k8s-workertools`)
- [Liquibase workertools](#liquibase-workertools) (`octopuslabs/liquibase-workertools`)
- [Terraform workertools](#terraform-workertools) (`octopuslabs/terraform-workertools`)
- [HashiCorp Vault workertools](#vault-workertools) (`octopuslabs/vault-workertools`)

### Base workertools

This is the base image which includes:

- Python3
- PowerShell Core
- The `octopus` [command line tool](https://github.com/OctopusDeploy/cli/blob/main/README.md) (written in `Go`)

A new image is built each time a new version of PowerShell Core is detected. The version numbers are based on the version of PowerShell Core.

#### Tags

- `octopuslabs/workertools:latest`
- `octopuslabs/workertools:VERSION`
- `octopuslabs/workertools:VERSION-win.2022`

You can retrieve a list of all available tags on [DockerHub](https://hub.docker.com/repository/docker/octopuslabs/workertools/tags).

### AWS workertools

This image contains all the necessary tooling to deploy to [AWS](https://aws.amazon.com/) with Octopus Deploy:

- AWS CLI
- AWS ECS
- AWS EKS CTL
- TerraForm
- AWS PowerShell Tools Common

A new image is built each time a new version of AWS CLI is detected. The version numbers will be based on the version of AWS CLI.

#### Tags

- `octopuslabs/aws-workertools:latest`
- `octopuslabs/aws-workertools:VERSION`
- `octopuslabs/aws-workertools:VERSION-win.2022`

You can retrieve a list of all available tags on [DockerHub](https://hub.docker.com/repository/docker/octopuslabs/aws-workertools/tags).

### Azure workertools

This image contains all the necessary tooling to deploy to [Azure](https://azure.com/) with Octopus Deploy:

- Azure CLI
- Azure PowerShell (Az Modules)
- TerraForm

A new image is built each time a new version of Azure CLI is detected. The version numbers will be based on the version of the Azure CLI.

#### Tags

- `octopuslabs/azure-workertools:latest`
- `octopuslabs/azure-workertools:VERSION`
- `octopuslabs/azure-workertools:VERSION-win.2022`

You can retrieve a list of all available tags on [DockerHub](https://hub.docker.com/repository/docker/octopuslabs/azure-workertools/tags).

### Flyway workertools

This image contains all the necessary tooling to use the execution container feature with Octopus Deploy when running commands using flyway. 

- OpenJDK v17 Java runtime
- Flyway

A new image is built each time a new version of flyway is detected. The version numbers will be based on the version of the Flyway tool.

#### Tags

- `octopuslabs/flyway-workertools:latest`
- `octopuslabs/flyway-workertools:VERSION`
- `octopuslabs/flyway-workertools:VERSION-win.2022`

You can retrieve a list of all available tags on [DockerHub](https://hub.docker.com/repository/docker/octopuslabs/azure-workertools/tags).

### GCP workertools

This image contains all the necessary tooling to deploy to [GCP](https://cloud.google.com/) with Octopus Deploy:

- Google Cloud SDK (`gcloud`)
- Terraform

A new image is built each time a new version of the Google Cloud SDK is detected. The version numbers will be based on the version of the GCloud CLI.

#### Tags

- `octopuslabs/gcp-workertools:latest`
- `octopuslabs/gcp-workertools:VERSION`
- `octopuslabs/gcp-workertools:VERSION-win.2022`

You can retrieve a list of all available tags on [DockerHub](https://hub.docker.com/repository/docker/octopuslabs/gcp-workertools/tags).

### Kubernetes workertools

This image contains all the necessary tooling to deploy to [Kubernetes](https://kubernetes.io/) with Octopus Deploy:

- Kubectl
- Helm
- AWS IAM Authenticator
- Google's GKE Cloud Auth Plugin

A new image is built each time a new version of `kubectl` is detected. The version numbers will be based on the version of `kubectl`.

#### Tags

- `octopuslabs/k8s-workertools:latest`
- `octopuslabs/k8s-workertools:VERSION`
- `octopuslabs/k8s-workertools:VERSION-win.2022`
- `octopuslabs/k8s-workertools:[VERSION-Major].[Version-Minor]`

You can retrieve a list of all available tags on [DockerHub](https://hub.docker.com/repository/docker/octopuslabs/k8s-workertools/tags).

### Liquibase workertools

This image contains all the necessary tooling to run Liquibase commands with Octopus Deploy:

- OpenJDK 17 Java runtime
- Liquibase

A new image is built each time a new version of Liqbuibase is detected. The version numbers will be based on the version of the Liquibase CLI.

> **Note:** No `windows/amd64` platform support is provided for this image.

#### Tags

- `octopuslabs/liquibase-workertools:latest`
- `octopuslabs/liquibase-workertools:VERSION`

You can retrieve a list of all available tags on [DockerHub](https://hub.docker.com/repository/docker/octopuslabs/liquibase-workertools/tags).

### Terraform workertools

This image contains all the necessary tooling to run [Terraform](https://terraform.io/) commands with Octopus Deploy:

- Git
- Terraform

A new image is built each time a new version of Terraform is detected. The version numbers will be based on the version of Terraform.

#### Tags

- `octopuslabs/terraform-workertools:latest`
- `octopuslabs/terraform-workertools:VERSION`
- `octopuslabs/terraform-workertools:VERSION-win.2022`

You can retrieve a list of all available tags on [DockerHub](https://hub.docker.com/repository/docker/octopuslabs/terraform-workertools/tags).

### Vault workertools

This image contains all the necessary tooling to run [HashiCorp Vault](https://www.vaultproject.io/) commands with Octopus Deploy:

- HashiCorp Vault

A new image is built each time a new version of HashiCorp Vault is detected. The version numbers will be based on the version of Vault.

> Note: No windows/amd64 platform support is provided for this image.

#### Tags

- `octopuslabs/vault-workertools:latest`
- `octopuslabs/vault-workertools:VERSION`

You can retrieve a list of all available tags on [DockerHub](https://hub.docker.com/repository/docker/octopuslabs/vault-workertools/tags).

## Support

Please consider this repository provided as is.  If there are any issues please do not contact support.
