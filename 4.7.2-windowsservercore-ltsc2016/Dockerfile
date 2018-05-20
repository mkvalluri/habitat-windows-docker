# escape=`

FROM microsoft/dotnet-framework:4.7.2-runtime-windowsservercore-ltsc2016
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop';"]

# Enable IIS, ASP.NET Frameworks
# Also remove default IIS Website and add Service Monitor
RUN Add-WindowsFeature Web-Server; `
    Add-WindowsFeature NET-Framework-45-ASPNET; `
    Add-WindowsFeature Web-Asp-Net45; `
    Remove-Item -Recurse C:\inetpub\wwwroot\*; `
	Remove-WebSite -Name 'Default Web Site' ; `
    Invoke-WebRequest -Uri https://dotnetbinaries.blob.core.windows.net/servicemonitor/2.0.1.3/ServiceMonitor.exe -OutFile C:\ServiceMonitor.exe


# Download Habitat CLI and setup path
RUN Invoke-WebRequest https://api.bintray.com/content/habitat/stable/windows/x86_64/hab-%24latest-x86_64-windows.zip?bt_package=hab-x86_64-windows -OutFile c:\hab-cli.zip ; `	
    Expand-Archive -Path c:\hab-cli.zip -DestinationPath c:\ ; `
    Move-Item "C:\hab-0.*" -Destination "C:\hab-cli" -Recurse ; `
    Remove-Item c:\hab-cli.zip -Force ; `
    Remove-Item c:\hab-0.* -Force ; `
    setx path '%path%;C:\hab-cli'

# Setup Habitat Supervisor
RUN hab pkg install core/windows-service; `
    hab pkg exec core/windows-service install; `
    hab pkg install core/hab-sup/0.55.0; 