# neo-cli-ubuntu

FROM ubuntu:16.04
MAINTAINER Jonatan <jonatan.blockchain@gmail.com>

ENV DOTNET_SDK_VERSION dotnet-sdk-2.0.0-linux-x64
ENV DOTNET_SDK_DOWNLOAD_URL https://aka.ms/$DOTNET_SDK_VERSION
ENV PATH="/opt/dotnet:${PATH}"

ENV NEOCLI_VERSION 2.1.0
ENV NEOCLI_SHA256 F73BECE48D80E7DDE51C6DE5150852925F28B55B135DB16BE22468CDFC08D9E5
ENV NEOCLI_RELEASE neo-cli-ubuntu.16.04-x64.zip
ENV NEOCLI_DOWNLOAD_URL https://github.com/neo-project/neo-cli/releases/download/v$NEOCLI_VERSION/$NEOCLI_RELEASE

RUN apt-get update \ 
    && apt-get -y install unzip dialog curl apt-transport-https ca-certificates

RUN apt-get -y install --no-install-recommends \
    libc6 \
    libcurl3 \
    libgcc1 \
    libgssapi-krb5-2 \
    libicu-dev \
    liblttng-ust0 \
    libssl1.0.0 \
    libstdc++6 \
    libunwind8 \
    libuuid1 \
    zlib1g

RUN apt-get -y install libleveldb-dev libleveldb1v5 \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sSL --output dotnet.tar.gz $DOTNET_SDK_DOWNLOAD_URL \
    && mkdir -p /opt/dotnet && tar zxf dotnet.tar.gz -C /opt/dotnet \
    && rm -rf dotnet.tar.gz

RUN curl -sSL --output neo-cli-ubuntu.zip $NEOCLI_DOWNLOAD_URL \
    && echo "$NEOCLI_SHA256 *neo-cli-ubuntu.zip" | sha256sum -c - \
    && unzip neo-cli-ubuntu.zip -d /opt/ \
    && rm -rf neo-cli-ubuntu.zip

EXPOSE 10333
WORKDIR /opt/neo-cli
ENTRYPOINT [ "dotnet", "neo-cli.dll" ]
