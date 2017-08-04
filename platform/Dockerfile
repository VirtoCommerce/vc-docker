# escape=`

FROM microsoft/aspnet:4.6.2
MAINTAINER Alexander Siniouguine <support@virtocommerce.com>

# Download latest platform release
ADD https://github.com/VirtoCommerce/vc-platform/releases/download/v2.13.14/VirtoCommerce.Platform.2.13.14.zip /VirtoCommerce.Platform.zip
RUN powershell -Command Expand-Archive VirtoCommerce.Platform.zip -DestinationPath C:\vc-platform
#COPY source c:\vc-platform

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

