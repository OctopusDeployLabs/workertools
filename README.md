# Worker Tools Base

This repository contains images that contain the bare minimum to use the execution container feature with Octopus Deploy.

- Python3
- PowerShell Core
- The *EAP* `octopus` [command line tool](https://github.com/OctopusDeploy/cli/blob/main/README.md) (written in `Go`)
- The `octo` [command line tool](https://github.com/OctopusDeploy/OctopusCLI/) (written in `C#`)

The following images are built in this repo:

- Ubuntu 22.04
- Ubuntu 20.04 (tagged `latest` in [DockerHub](https://hub.docker.com/r/octopuslabs/workertools/tags?page=1&name=latest))
- Windows 2022 (tagged `latest` in [DockerHub](https://hub.docker.com/r/octopuslabs/workertools/tags?page=1&name=latest))

> Note: As Windows 2019 [mainstream support end date is Jan 9th, 2024](https://learn.microsoft.com/en-us/lifecycle/products/windows-server-2019), any `windows.2019` tagged images are no longer maintained.

A new image will be built each time a new version of PowerShell Core is created.  The version numbers will be based on the version of PowerShell Core.

**Please consider this repository provided as is.  If there are any issues please do not contact support.**
