# escape=`
ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest
SHELL ["powershell", "-Command"]

ARG FLYWAY_VERSION=10.7.1

# Get SQL Fluff for Flyway Check Command
RUN pip3 install sqlfluff==1.2.1

# # Install Flyway
RUN Invoke-WebRequest "https://download.red-gate.com/maven/release/com/redgate/flyway/flyway-commandline/${env:FLYWAY_VERSION}/flyway-commandline-${env:FLYWAY_VERSION}-windows-x64.zip" -OutFile flyway-cli.zip; `
    & '.\Program Files\7-Zip\7z.exe' x .\flyway-cli.zip; `
    rm .\flyway-cli.zip;
   
RUN $old = (Get-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path).path; `
    Write-Host $old; `
    $flywayPath = ';C:\flyway-' + ${env:FLYWAY_VERSION}; `    
    $new = $old + $flywayPath; `
    Write-Host $new; `
    Set-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path -Value $new; `
    Import-Module $env:ChocolateyInstall\helpers\chocolateyProfile.psm1; `
    refreshenv