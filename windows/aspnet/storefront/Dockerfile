# escape=`

FROM microsoft/aspnet:4.6.2
MAINTAINER Alexander Siniouguine <support@virtocommerce.com>

# Download latest platform release
RUN $var=Invoke-RestMethod -Method Get -Uri https://api.github.com/repos/virtocommerce/vc-storefront/releases/latest | select -ExpandProperty assets | ? { $_.name.Contains('VirtoCommerce.StoreFront')} | select -expand browser_download_url; wget $var -OutFile c:\VirtoCommerce.StoreFront.zip

RUN powershell.exe -Command `
    Expand-Archive VirtoCommerce.StoreFront.zip -DestinationPath C:\vc-storefront; `
    Remove-Item c:\VirtoCommerce.StoreFront.zip -Force

RUN Invoke-WebRequest "https://download.microsoft.com/download/2/E/6/2E61CFA4-993B-4DD4-91DA-3737CD5CD6E3/vcredist_x64.exe" -OutFile "c:\vc_redist.x64.exe"

RUN powershell start-process C:\vc_redist.x64.exe -ArgumentList '/quiet' -Wait

# Configure website
RUN Remove-Website -Name 'Default Web Site'; `  
    New-Website -Name 'vc-storefront' `
                -Port 80 -PhysicalPath 'c:\vc-storefront' `
                -ApplicationPool 'DefaultAppPool'