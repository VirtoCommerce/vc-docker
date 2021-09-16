FROM mcr.microsoft.com/dotnet/aspnet:5.0

COPY publish /opt/virtocommerce/platform

COPY ./wait-for-it.sh /wait-for-it.sh
RUN chmod +x wait-for-it.sh
RUN apt-get update && apt-get install -y wget fontconfig libfreetype6 libx11-6 libxcb1 libxext6 libxrender1 xfonts-75dpi xfonts-base libjpeg62-turbo \
    && wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.buster_amd64.deb && dpkg -i wkhtmltox_0.12.6-1.buster_amd64.deb

WORKDIR /opt/virtocommerce/platform

ENTRYPOINT ["dotnet", "VirtoCommerce.Platform.Web.dll"]