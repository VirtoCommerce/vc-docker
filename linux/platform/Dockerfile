FROM mcr.microsoft.com/dotnet/core/aspnet:3.1

#RUN apt-get update
#RUN apt-get -yq install wget \
#    && apt-get -yq install unzip

COPY publish /opt/virtocommerce/platform
#RUN wget -q "https://github.com/VirtoCommerce/vc-platform/releases/download/3.0.0-rc.4/VirtoCommerce.Platform.3.0.0-rc.4.167.zip" \
#    && unzip -q VirtoCommerce.Platform.3.0.0-rc.4.167.zip -d /opt/virtocommerce/platform \
#    && rm VirtoCommerce.Platform.3.0.0-rc.4.167.zip

# Uncomment this line to enable running in Alpine distributions
# RUN apk add icu-libs
# ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false

COPY ./wait-for-it.sh /wait-for-it.sh
RUN chmod +x wait-for-it.sh
RUN apt-get update && apt-get install -y wget fontconfig libfreetype6 libx11-6 libxcb1 libxext6 libxrender1 xfonts-75dpi xfonts-base libjpeg62-turbo \
    && wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.buster_amd64.deb && dpkg -i wkhtmltox_0.12.6-1.buster_amd64.deb

WORKDIR /opt/virtocommerce/platform

ENTRYPOINT ["dotnet", "VirtoCommerce.Platform.Web.dll"]