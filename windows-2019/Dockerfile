# escape=`

FROM mcr.microsoft.com/windows/servercore:ltsc2019
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
    refreshenv

# # Install legacy Octo CLI
RUN choco install octopustools -y --no-progress; `
    refreshenv

# # Install vNext Octo CLI
RUN choco install octopus-cli -y --no-progress; `
    refreshenv