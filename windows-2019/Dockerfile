# escape=`

# We have to use the .NET Framework base image in place of mcr.microsoft.com/windows/servercore:ltsc2019
# As chocolately v2 requires .NET 4.8. See https://docs.chocolatey.org/en-us/guides/upgrading-to-chocolatey-v2-v6#net-framework-4.8-required
# Note: .NET 4.8.1 is not supported on Win2019, only Win2022+. See https://devblogs.microsoft.com/dotnet/announcing-dotnet-framework-481/
FROM mcr.microsoft.com/dotnet/framework/runtime:4.8-windowsservercore-ltsc2019
SHELL ["powershell", "-Command"]

# Install Choco
RUN $ProgressPreference = 'SilentlyContinue'; `
    Set-ExecutionPolicy Bypass -Scope Process -Force; `
    [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
    iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

# # Install 7ZIP
RUN choco install 7zip -y --no-progress

# # Install Powershell Core
RUN choco install powershell-core -y --no-progress

# # Install python
RUN choco install -y python3 --no-progress; `
    Import-Module $env:ChocolateyInstall\helpers\chocolateyProfile.psm1; `
    refreshenv

# # Install legacy Octo CLI
RUN choco install octopustools -y --no-progress; `
    Import-Module $env:ChocolateyInstall\helpers\chocolateyProfile.psm1; `
    refreshenv

# # Install vNext Octo CLI
RUN choco install octopus-cli -y --no-progress; `
    Import-Module $env:ChocolateyInstall\helpers\chocolateyProfile.psm1; `
    refreshenv