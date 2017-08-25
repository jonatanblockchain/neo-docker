# neo-cli-windows

FROM microsoft/nanoserver
MAINTAINER Jonatan <jonatan.blockchain@gmail.com>

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ENV DOTNET_SDK_VERSION 2.0.0
ENV DOTNET_SDK_DOWNLOAD_URL https://dotnetcli.blob.core.windows.net/dotnet/Sdk/$DOTNET_SDK_VERSION/dotnet-sdk-$DOTNET_SDK_VERSION-win-x64.zip
ENV DOTNET_SDK_DOWNLOAD_SHA C0942299437541C6B173F71213B43D2CC1E0EBC5C75F78948C0C6279A8D1C5B293999C93863392A4219F819B1DDD73D95112930B08EC8DDAA89918931E492DB0

ENV NEOCLI_VERSION 2.1.0
ENV NEOCLI_SHA256 12BBDA6832AD7737FD57C0E8C47C43B656DE53EE69E174C0E9C93D6458944E5A
ENV NEOCLI_RELEASE neo-cli-win10-x64.zip
ENV NEOCLI_DOWNLOAD_URL https://github.com/neo-project/neo-cli/releases/download/v$NEOCLI_VERSION/$NEOCLI_RELEASE

RUN Invoke-WebRequest $Env:DOTNET_SDK_DOWNLOAD_URL -OutFile dotnet.zip; \
    if ((Get-FileHash dotnet.zip -Algorithm sha512).Hash -ne $Env:DOTNET_SDK_DOWNLOAD_SHA) { \
        Write-Host 'CHECKSUM VERIFICATION FAILED!'; \
        exit 1; \
    }; \
    \
    Expand-Archive dotnet.zip -DestinationPath $Env:ProgramFiles\dotnet; \
    Remove-Item -Force dotnet.zip

RUN setx /M PATH $($Env:PATH + ';' + $Env:ProgramFiles + '\dotnet')

RUN Invoke-WebRequest $Env:NEOCLI_DOWNLOAD_URL -OutFile neo-cli-win10.zip; \
    if ((Get-FileHash neo-cli-win10.zip -Algorithm sha256).Hash -ne $Env:NEOCLI_SHA256) { \
        Write-Host 'CHECKSUM VERIFICATION FAILED!'; \
        exit 1; \
    }; \
    \
    Expand-Archive neo-cli-win10.zip -DestinationPath $Env:SystemDrive; \
    Remove-Item -Force neo-cli-win10.zip

EXPOSE 10333
WORKDIR c:\\neo-cli
ENTRYPOINT [ "dotnet", "neo-cli.dll" ]
