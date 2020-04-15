FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine

#RUN apt-get update
#RUN apt-get -yq install wget \
#    && apt-get -yq install unzip

COPY publish /opt/virtocommerce/platform
#RUN wget -q "https://github.com/VirtoCommerce/vc-platform/releases/download/3.0.0-rc.4/VirtoCommerce.Platform.3.0.0-rc.4.167.zip" \
#    && unzip -q VirtoCommerce.Platform.3.0.0-rc.4.167.zip -d /opt/virtocommerce/platform \
#    && rm VirtoCommerce.Platform.3.0.0-rc.4.167.zip

RUN apk add icu-libs
ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false

WORKDIR /opt/virtocommerce/platform

ENTRYPOINT ["dotnet", "VirtoCommerce.Platform.Web.dll"]