FROM mcr.microsoft.com/dotnet/aspnet:10.0

COPY ./wait-for-it.sh /wait-for-it.sh
RUN chmod +x /wait-for-it.sh

RUN apt-get update && \
    apt-get install -y --no-install-recommends wkhtmltopdf && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    wkhtmltopdf --version


COPY publish /opt/virtocommerce/platform

RUN find /opt/virtocommerce/platform/modules -path "*/bin/runtimes/linux-x64/**/*" -type f \
    -exec cp "{}" /opt/virtocommerce/platform/app_data/modules/ \; || true

WORKDIR /opt/virtocommerce/platform
EXPOSE 80
ENV ASPNETCORE_HTTP_PORTS=80

ENTRYPOINT ["dotnet", "VirtoCommerce.Platform.Web.dll"]
