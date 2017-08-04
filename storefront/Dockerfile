# escape=`

FROM microsoft/aspnet:4.6.2
MAINTAINER Alexander Siniouguine <support@virtocommerce.com>

# Install Visual C++ Redistributable Packages
# ADD https://download.microsoft.com/download/6/A/A/6AA4EDFF-645B-48C5-81CC-ED5963AEAD48/vc_redist.x64.exe /vc_redist.x64.exe
ADD https://download.microsoft.com/download/2/E/6/2E61CFA4-993B-4DD4-91DA-3737CD5CD6E3/vcredist_x64.exe /vc_redist.x64.exe
ADD https://download.microsoft.com/download/2/E/6/2E61CFA4-993B-4DD4-91DA-3737CD5CD6E3/vcredist_x86.exe /vc_redist.x86.exe

RUN C:\vc_redist.x64.exe /quiet /install
RUN C:\vc_redist.x86.exe /quiet /install

# Configure website
RUN Remove-Website -Name 'Default Web Site'; `  
    md c:\vc-storefront; `
    New-Website -Name 'vc-storefront' `
                -Port 80 -PhysicalPath 'c:\vc-storefront' `
                -ApplicationPool 'DefaultAppPool'

COPY source c:\vc-storefront