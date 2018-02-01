#neo-cli-windows10

FROM microsoft/dotnet:2.0-sdk-nanoserver
MAINTAINER Jonatan <jonatan.blockchain@gmail.com>

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ENV NEOCLI_VERSION 2.7.1
ENV NEOCLI_SHA256 291ECAC320F6B07DF640206E67CE952444D06E7E6CFC3848BB911F9C2D9EAE6C
ENV NEOCLI_RELEASE neo-cli-win10-x64.zip
ENV NEOCLI_DOWNLOAD_URL https://github.com/neo-project/neo-cli/releases/download/v$NEOCLI_VERSION/$NEOCLI_RELEASE

RUN Invoke-WebRequest $Env:NEOCLI_DOWNLOAD_URL -OutFile neo-cli-win10.zip; \
    if ((Get-FileHash neo-cli-win10.zip -Algorithm sha256).Hash -ne $Env:NEOCLI_SHA256) { \
        Write-Host 'CHECKSUM VERIFICATION FAILED!'; \
        exit 1; \
    }; \
    \
    Expand-Archive neo-cli-win10.zip -DestinationPath $Env:SystemDrive; \
    Remove-Item -Force neo-cli-win10.zip

#libdeveldb missing?

EXPOSE 10333
WORKDIR c:\\neo-cli
ENTRYPOINT [ "dotnet", "neo-cli.dll" ]
