# escape=`
# Build runtime image
FROM microsoft/aspnetcore:2.0
MAINTAINER Alexander Siniouguine <support@virtocommerce.com>

ARG SOURCE=VirtoCommerce.Storefront\bin\Debug\netcoreapp2.0\publish
WORKDIR /app
COPY $SOURCE .
ENTRYPOINT ["dotnet", "VirtoCommerce.Storefront.dll"]