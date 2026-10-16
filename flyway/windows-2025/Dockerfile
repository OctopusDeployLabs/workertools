# escape=`
ARG BASE_IMAGE=octopuslabs/workertools
FROM ${BASE_IMAGE}:latest
SHELL ["powershell", "-Command"]

ARG FLYWAY_VERSION=13.10.3

# SQLFluff for Flyway's check -code command ships with the Flyway CLI (11.10+, on by default from 11.16)
# as a self-contained runner, so it doesn't need installing separately.

# # Install Flyway
RUN Invoke-WebRequest "https://download.red-gate.com/maven/release/com/redgate/flyway/flyway-commandline/${env:FLYWAY_VERSION}/flyway-commandline-${env:FLYWAY_VERSION}-windows-x64.zip" -OutFile flyway-cli.zip; `
    & '.\Program Files\7-Zip\7z.exe' x .\flyway-cli.zip; `
    rm .\flyway-cli.zip;

# Install mongosh
RUN Invoke-WebRequest "https://downloads.mongodb.com/compass/mongosh-2.10.0-win32-x64.zip" -Outfile "mongosh.zip"; `
  & '.\Program Files\7-Zip\7z.exe' x .\mongosh.zip; `
  rm .\mongosh.zip
   
RUN $old = (Get-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path).path; `
    Write-Host $old; `
    $flywayPath = ';C:\flyway-' + ${env:FLYWAY_VERSION}; `
    $monoshPath = ';C:\mongosh'; `    
    $new = $old + $flywayPath + $mongosh; `
    Write-Host $new; `
    Set-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment' -Name path -Value $new; `
    Import-Module $env:ChocolateyInstall\helpers\chocolateyProfile.psm1; `
    refreshenv