# escape=`

FROM microsoft/dotnet-framework:4.7.2-runtime-windowsservercore-1803
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop';"]

# Download Habitat CLI and setup path
RUN Invoke-WebRequest https://api.bintray.com/content/habitat/stable/windows/x86_64/hab-%24latest-x86_64-windows.zip?bt_package=hab-x86_64-windows -OutFile c:\hab-cli.zip ; `	
    Expand-Archive -Path c:\hab-cli.zip -DestinationPath c:\ ; `
    Move-Item "C:\hab-0.*" -Destination "C:\hab-cli" ; `
    Remove-Item c:\hab-cli.zip -Force ; `
    Remove-Item c:\hab-0.* -Force ; `
    setx path '%path%;C:\hab-cli'

# Setup Habitat Supervisor
RUN hab pkg install core/windows-service; `
    hab pkg exec core/windows-service install; `
    hab pkg install core/hab-sup/0.56.0; 