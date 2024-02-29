FROM mcr.microsoft.com/dotnet/aspnet:8.0

# RUN apt-get update
# RUN apt-get -yq install wget \
#    && apt-get -yq install unzip

COPY publish /opt/virtocommerce/platform
# RUN wget -q "https://github.com/VirtoCommerce/vc-platform/releases/download/3.809.0/VirtoCommerce.Platform.3.809.0.zip"
# RUN mkdir -p /opt/virtocommerce/platform
# RUN unzip -q VirtoCommerce.Platform.3.809.0.zip -d /opt/virtocommerce/platform
# RUN rm VirtoCommerce.Platform.3.809.0.zip

# Uncomment this line to enable running in Alpine distributions
# RUN apk add icu-libs
# ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false

COPY ./wait-for-it.sh /wait-for-it.sh
RUN chmod +x wait-for-it.sh
RUN apt-get update && apt-get install -y wget fontconfig libfreetype6 libx11-6 libxcb1 libxext6 libxrender1 xfonts-75dpi xfonts-base libjpeg62-turbo \
  && wget http://http.us.debian.org/debian/pool/main/o/openssl/libssl3_3.0.11-1~deb12u2_amd64.deb \
  && dpkg -i libssl3_3.0.11-1~deb12u2_amd64.deb \
  && wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-3/wkhtmltox_0.12.6.1-3.bookworm_amd64.deb \
  && dpkg -i wkhtmltox_0.12.6.1-3.bookworm_amd64.deb

WORKDIR /opt/virtocommerce/platform
EXPOSE 80
ENV ASPNETCORE_HTTP_PORTS=80
ENTRYPOINT ["dotnet", "VirtoCommerce.Platform.Web.dll"]  
