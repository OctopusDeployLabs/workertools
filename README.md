# Worker Tools Base

This repository contains images that contain the bare minimum to use the execution container feature with Octopus Deploy.

- Python3
- PowerShell Core
- The *EAP* `octopus` [command line tool](https://github.com/OctopusDeploy/cli/blob/main/README.md) (written in `Go`)
- The `octo` [command line tool](https://github.com/OctopusDeploy/OctopusCLI/) (written in `C#`)

The following images are built in this repo:

- Ubuntu 22.04
- Ubuntu 20.04
- Windows 2022

A new image will be built each time a new version of PowerShell Core is created.  The version numbers will be based on the version of PowerShell Core.

## Deprecated tags

Please note the following tags are no longer maintained:
- Any images tagged with `windows.2019` as Windows 2019 [mainstream support end date is Jan 9th, 2024](https://learn.microsoft.com/en-us/lifecycle/products/windows-server-2019)
- Any images tagged with `latest`. 

> **For backwards compatibility, images tagged with `latest` are still available in DockerHub. They are built on Ubuntu 20.04, Ubuntu 22.04 and Windows 2019.**

## Support

Please consider this repository provided as is.  If there are any issues please do not contact support.
