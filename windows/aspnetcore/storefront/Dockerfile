# escape=`
# Build runtime image
FROM microsoft/aspnetcore:2.0
MAINTAINER Alexander Siniouguine <support@virtocommerce.com>
ARG SOURCE=VirtoCommerce.Storefront\bin\Debug\netcoreapp2.0\publish
WORKDIR /app
COPY $SOURCE .
COPY libs\x64\msvcp140.dll c:\windows\system32
COPY libs\x64\vcruntime140.dll c:\windows\system32
ENTRYPOINT ["dotnet", "VirtoCommerce.Storefront.dll"]