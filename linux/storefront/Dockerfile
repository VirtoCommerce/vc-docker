	# escape=`
# Build runtime image
FROM microsoft/dotnet:2.2-aspnetcore-runtime-alpine
MAINTAINER Alexander Siniouguine <support@virtocommerce.com>

# Install unzip
#RUN apt-get update && apt-get install -y unzip
#RUN apt-get update -qq `
#&& apt-get install -y wget

COPY publish /opt/virtocommerce/storefront
#RUN mkdir -p /opt/virtocommerce/storefront `
#    && curl -s https://api.github.com/repos/virtocommerce/vc-storefront-core/releases/latest `
#	| grep "browser_download_url.*zip" `
#	| cut -d : -f 2,3 `
#	| tr -d \" `
#	| wget -qi - `
#	&& sh -c 'unzip -q -d /opt/virtocommerce/storefront "*.zip"' `
#	&& sh -c 'rm *.zip'

RUN apk add icu-libs
ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false

RUN mkdir -p /opt/virtocommerce/storefront/wwwroot/cms-content
WORKDIR /opt/virtocommerce/storefront
ENTRYPOINT ["dotnet", "VirtoCommerce.Storefront.dll"]