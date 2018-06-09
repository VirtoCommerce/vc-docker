# escape=`
# Build runtime image
FROM microsoft/dotnet:2.1-aspnetcore-runtime
MAINTAINER Alexander Siniouguine <support@virtocommerce.com>

# download latest release
RUN $var=Invoke-RestMethod -Method Get -Uri https://api.github.com/repos/virtocommerce/vc-storefront-core/releases/latest | select -ExpandProperty assets | ? { $_.name.Contains('VirtoCommerce.StoreFront')} | select -expand browser_download_url; Invoke-WebRequest $var -OutFile c:\VirtoCommerce.StoreFront.zip

RUN powershell.exe -Command `
    Expand-Archive VirtoCommerce.StoreFront.zip -DestinationPath C:\vc-storefront; `
    Remove-Item c:\VirtoCommerce.StoreFront.zip -Force

# download latest default theme
# RUN $var=Invoke-RestMethod -Method Get -Uri https://api.github.com/repos/virtocommerce/vc-theme-default/releases/latest | select -ExpandProperty assets | ? { $_.name.Contains('vc-default-theme')} | select -expand browser_download_url; Invoke-WebRequest $var -OutFile c:\vc-default-theme.zip

# RUN powershell.exe -Command `
#     Expand-Archive vc-default-theme.zip -DestinationPath C:\vc-storefront\wwwroot\cms-content\themes\electronics; `
#     Remove-Item c:\vc-default-theme.zip -Force

# download latest material theme
# RUN $var=Invoke-RestMethod -Method Get -Uri https://api.github.com/repos/virtocommerce/vc-theme-material/releases/latest | select -ExpandProperty assets | ? { $_.name.Contains('vc-material-theme')} | select -expand browser_download_url; Invoke-WebRequest $var -OutFile c:\vc-theme-material.zip

# RUN powershell.exe -Command `
#     Expand-Archive vc-theme-material.zip -DestinationPath C:\vc-storefront\wwwroot\cms-content\themes\clothing; `
#     Remove-Item c:\vc-theme-material.zip -Force

WORKDIR /vc-storefront
COPY libs\x64\msvcp140.dll c:\windows\system32
COPY libs\x64\vcruntime140.dll c:\windows\system32
ENTRYPOINT ["dotnet", "VirtoCommerce.Storefront.dll"]