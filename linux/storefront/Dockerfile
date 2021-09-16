	# escape=`
# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:5.0

COPY publish /opt/virtocommerce/storefront

RUN mkdir -p /opt/virtocommerce/storefront/wwwroot/cms-content
WORKDIR /opt/virtocommerce/storefront
ENTRYPOINT ["dotnet", "VirtoCommerce.Storefront.dll"]
