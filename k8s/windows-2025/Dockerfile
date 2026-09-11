# escape=`
ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest
SHELL ["powershell", "-Command"]

# gcloud cli needed for gke auth plugin
ARG GCLOUD_CLI_VERSION=433.0.0

RUN choco install kubernetes-cli -y --no-progress

RUN choco install -y kubernetes-helm --no-progress

# install sops and helm-secrets
RUN $pluginsDir = Join-Path $env:APPDATA "helm/plugins"; `
    $pluginDir = Join-Path $pluginsDir "secrets"; `
    $tempFile = Join-Path $env:TEMP "helm-secrets.tar.gz"; `
    New-Item -Path $pluginDir -ItemType Directory -Force | Out-Null; `
    Invoke-WebRequest -Uri "https://github.com/jkroepke/helm-secrets/releases/latest/download/helm-secrets.tar.gz" -OutFile $tempFile; `
    tar -xzf $tempFile -C $pluginDir; `
    Remove-Item $tempFile -Force;
RUN choco install sops -y --no-progress

# Get Kubelogin
RUN choco install azure-kubelogin --no-progress -y

RUN choco install eksctl -y --no-progress

RUN choco install awscli -y --no-progress

# Get Argo
RUN choco install argocd-cli -y --no-progress

# Install Azure CLI
RUN choco install azure-cli -y --no-progress

RUN Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force; `
    Install-Module -Force -Name Az -AllowClobber -Scope AllUsers

# Install gcloud (required for gke-auth-plugin)
RUN $GCLOUD_VERSION = $env:GCLOUD_CLI_VERSION; `
    Write-Host "GCLOUD_VERSION: ${env:GCLOUD_CLI_VERSION}"; `
    Write-Host "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${env:GCLOUD_CLI_VERSION}-windows-x86_64.zip"; `
    Invoke-WebRequest "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${env:GCLOUD_CLI_VERSION}-windows-x86_64.zip" -OutFile google-cloud-sdk-$env:GCLOUD_CLI_VERSION-windows-x86_64.zip; `
    & '.\Program Files\7-Zip\7z.exe' x .\google-cloud-sdk-$env:GCLOUD_CLI_VERSION-windows-x86_64.zip; `
    .\google-cloud-sdk\install.bat --quiet; `
    rm .\google-cloud-sdk-$env:GCLOUD_CLI_VERSION-windows-x86_64.zip

# Update Path
RUN $old = (Get-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path).path; `
    Write-Host $old; `
    $gcloudPath = ';C:\google-cloud-sdk\bin'; `    
    $new = $old + $gcloudPath; `
    Write-Host $new; `
    Set-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path -Value $new; `
    Import-Module $env:ChocolateyInstall\helpers\chocolateyProfile.psm1; `
    refreshenv

# Install gke-gcloud-auth-plugin (gcloud cli doesnt make this easy)
RUN Write-Host "Installing gke-gcloud-auth-plugin"; ` 
    $env:CLOUDSDK_PYTHON = (& gcloud components copy-bundled-python); `
    Write-Host "GCLOUDSDK_PYTHON path: ${env:CLOUDSDK_PYTHON}"; `
    $env:GCloud_output = (gcloud components install gke-gcloud-auth-plugin --quiet 2>&1); `
    if(-not [string]::IsNullOrWhiteSpace($env:GCloud_output)) { Write-Host "${env:GCloud_output}"; }
