FROM mcr.microsoft.com/dotnet/core/aspnet:3.1.1-bionic

RUN apt-get update
RUN apt-get -yq install wget \
    && apt-get -yq install unzip

RUN wget -q "https://github.com/VirtoCommerce/vc-platform/releases/download/3.0.0-rc.3/VirtoCommerce.Platform.3.0.0-rc.3.1.zip" \
    && unzip -q VirtoCommerce.Platform.3.0.0-rc.3.1.zip -d vc-platform-3 \
    && rm VirtoCommerce.Platform.3.0.0-rc.3.1.zip

WORKDIR /vc-platform-3

ENTRYPOINT ["dotnet", "VirtoCommerce.Platform.Web.dll"]