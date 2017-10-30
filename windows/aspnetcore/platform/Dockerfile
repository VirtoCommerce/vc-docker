# escape=`

FROM microsoft/aspnet:4.6.2
MAINTAINER Alexander Siniouguine <support@virtocommerce.com>

# Download latest platform release
RUN $var=Invoke-RestMethod -Method Get -Uri https://api.github.com/repos/virtocommerce/vc-platform/releases/latest | select -ExpandProperty assets | ? { $_.name.Contains('VirtoCommerce.Platform')} | select -expand browser_download_url; wget $var -OutFile c:\VirtoCommerce.Platform.zip
RUN powershell.exe -Command `
    Expand-Archive VirtoCommerce.Platform.zip -DestinationPath C:\vc-platform; `
    Remove-Item c:\VirtoCommerce.Platform.zip -Force

# Configure website
RUN Remove-Website -Name 'Default Web Site'; `  
    md c:\vc-platform\App_Data\Assets; `
    md C:\vc-platform\App_Data\Modules; `
    md C:\vc-platform\Modules; `
    New-Website -Name 'vc-platform' `
                -Port 80 -PhysicalPath 'c:\vc-platform' `
                -ApplicationPool 'DefaultAppPool'

RUN c:\windows\system32\inetsrv\appcmd add vdir "/app.name:'vc-platform/'" /path:/assets /physicalPath:c:\vc-platform\app_data\assets; `
    icacls C:\inetpub\wwwroot\App_Data /t /grant "Users:W"; `
    icacls C:\inetpub\wwwroot\Modules /t /grant "Users":W;

