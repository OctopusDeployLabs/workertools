# escape=`
ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest
SHELL ["powershell", "-Command"]

ARG JFROG_CLI_VERSION=2.78.3
ENV JFROG_CLI_VERSION=${JFROG_CLI_VERSION}
ENV JFROG_HOME="C:\jfrog-cli"

# Download JFrog CLI, move to install location, and update PATH
RUN New-Item -ItemType Directory -Path $env:JFROG_HOME | Out-Null ; `
    Invoke-WebRequest -Uri "https://releases.jfrog.io/artifactory/jfrog-cli/v2-jf/${env:JFROG_CLI_VERSION}/jfrog-cli-windows-amd64/jf.exe" -OutFile "c:\jfrog-cli\jf.exe" ; `
    $old = (Get-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path).path; `
    Write-Host $old; `
    $jFrogPath = ';C:\jfrog-cli'; `    
    $new = $old + $jFrogPath; `
    Write-Host $new; `
    Set-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path -Value $new; `
    refreshenv