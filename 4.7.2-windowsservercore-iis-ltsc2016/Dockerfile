# escape=`

FROM mkvalluri/habitat-windows:0.56
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop';"]

# Enable IIS, ASP.NET Frameworks
# Also remove default IIS Website and add Service Monitor
RUN Add-WindowsFeature Web-Server; `
    Add-WindowsFeature NET-Framework-45-ASPNET; `
    Add-WindowsFeature Web-Asp-Net45; `
    Remove-Item -Recurse C:\inetpub\wwwroot\*; `
	Remove-WebSite -Name 'Default Web Site' ; `
    Invoke-WebRequest -Uri https://dotnetbinaries.blob.core.windows.net/servicemonitor/2.0.1.3/ServiceMonitor.exe -OutFile C:\ServiceMonitor.exe


# Install xWebAdministration
RUN Install-PackageProvider -Name NuGet -Force | Out-Null; `
    Install-Module xWebAdministration -Force | Out-Null ;