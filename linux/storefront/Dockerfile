# escape=`
# Build runtime image
FROM microsoft/dotnet:2.1-aspnetcore-runtime
MAINTAINER Alexander Siniouguine <support@virtocommerce.com>

# Install unzip
RUN apt-get update && apt-get install -y unzip
RUN apt-get update -qq `
&& apt-get install -y wget

RUN mkdir -p /vc-storefront `
    && curl -s https://api.github.com/repos/virtocommerce/vc-storefront-core/releases/latest `
	| grep "browser_download_url.*zip" `
	| cut -d : -f 2,3 `
	| tr -d \" `
	| wget -qi - `
	&& sh -c 'unzip -q -d /vc-storefront "*.zip"' `
	&& sh -c 'rm *.zip'

WORKDIR /vc-storefront
ENTRYPOINT ["dotnet", "VirtoCommerce.Storefront.dll"]