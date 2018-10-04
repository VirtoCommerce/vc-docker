# escape=`
# Build runtime image
FROM microsoft/dotnet:2.1-aspnetcore-runtime

#download JQ / json tool
RUN curl.exe -o jq.exe "https://github.com/stedolan/jq/releases/download/jq-1.5/jq-win64.exe" -L

# download and unzip latest release, nano doesn't support powershell, so use curl and tar instead
RUN curl -s https://api.github.com/repos/virtocommerce/vc-storefront-core/releases/latest | jq -r ".assets[] | select(.name | test(\"VirtoCommerce.StoreFront\")) | .browser_download_url" > download.txt

# we can use the following command instead of download.txt
# echo --url "google.com" | curl --config -

RUN for /f "eol=;" %i in (download.txt) do curl -o VirtoCommerce.StoreFront.zip %i -L `
    && mkdir -p vc-storefront `
    && tar -zxf VirtoCommerce.StoreFront.zip -C c:\vc-storefront `
    && del VirtoCommerce.StoreFront.zip

WORKDIR /vc-storefront
#Nano server doesn't support installs, need to copy DLLs manually
COPY libs\x64\*.dll c:\windows\SysWOW64\
COPY libs\x86\*.dll c:\windows\System32\
ENTRYPOINT ["dotnet", "VirtoCommerce.Storefront.dll"]
