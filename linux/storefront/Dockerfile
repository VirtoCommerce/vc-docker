# escape=`
# Build runtime image
FROM microsoft/dotnet:2.1-aspnetcore-runtime
MAINTAINER Alexander Siniouguine <support@virtocommerce.com>

# download latest release
RUN $var=Invoke-RestMethod -Method Get -Uri https://api.github.com/repos/virtocommerce/vc-storefront-core/releases/latest | select -ExpandProperty assets | ? { $_.name.Contains('VirtoCommerce.StoreFront')} | select -expand browser_download_url; wget $var -OutFile c:\VirtoCommerce.StoreFront.zip

RUN powershell.exe -Command `
    Expand-Archive VirtoCommerce.StoreFront.zip -DestinationPath C:\vc-storefront-core; `
    Remove-Item c:\VirtoCommerce.StoreFront.zip -Force

WORKDIR /vc-storefront-core
ENTRYPOINT ["dotnet", "VirtoCommerce.Storefront.dll"]