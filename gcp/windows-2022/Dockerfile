# escape=`
ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest
SHELL ["powershell", "-Command"]

ARG GOOGLE_CLOUD_CLI_VERSION=462.0.0

# Install Terraform
RUN choco install terraform -y --no-progress

# Install gcloud
RUN $GCLOUD_VERSION = $env:GOOGLE_CLOUD_CLI_VERSION; `
    Write-Host "GCLOUD_VERSION: ${env:GOOGLE_CLOUD_CLI_VERSION}"; `
    Write-Host "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${env:GOOGLE_CLOUD_CLI_VERSION}-windows-x86_64.zip"; `
    Invoke-WebRequest "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${env:GOOGLE_CLOUD_CLI_VERSION}-windows-x86_64.zip" -OutFile google-cloud-sdk-$env:GOOGLE_CLOUD_CLI_VERSION-windows-x86_64.zip; `
    & '.\Program Files\7-Zip\7z.exe' x .\google-cloud-sdk-$env:GOOGLE_CLOUD_CLI_VERSION-windows-x86_64.zip; `
    .\google-cloud-sdk\install.bat --quiet; `
    rm .\google-cloud-sdk-$env:GOOGLE_CLOUD_CLI_VERSION-windows-x86_64.zip

# Update Path
RUN $old = (Get-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path).path; `
    Write-Host $old; `
    $gcloudPath = ';C:\google-cloud-sdk\bin'; `    
    $new = $old + $gcloudPath; `
    Write-Host $new; `
    Set-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path -Value $new; `
    Import-Module $env:ChocolateyInstall\helpers\chocolateyProfile.psm1; `
    refreshenv