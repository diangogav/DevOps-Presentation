```dockerfile
#msbuild.Dockerfile
FROM mcr.microsoft.com/windows/servercore:1709

# Install Chocolatey
RUN @powershell -NoProfile -ExecutionPolicy Bypass -Command "$env:ChocolateyUseWindowsCompression='false'; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

# Install build tools
RUN powershell add-windowsfeature web-asp-net45 ; `
choco install microsoft-build-tools -y --allow-empty-checksums -version 14.0.23107.10 ; `
choco install dotnet4.6-targetpack --allow-empty-checksums -y ; `
choco install nuget.commandline --allow-empty-checksums -y ; `
choco install netfx-4.5.1-devpack --allow-empty-checksums -y ; `
nuget install MSBuild.Microsoft.VisualStudio.Web.targets -Version 14.0.0.3 ; `
nuget install WebConfigTransformRunner -Version 1.0.0.1

RUN powershell remove-item C:\inetpub\wwwroot\iisstart.*

```