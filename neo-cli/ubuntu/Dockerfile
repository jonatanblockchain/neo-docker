FROM centos:centos7
LABEL maintainer="Jonatan/Blockchain"

ENV DOTNET_SDK_VERSION dotnet-sdk-2.0.0-linux-x64
ENV DOTNET_SDK_DOWNLOAD_URL https://aka.ms/$DOTNET_SDK_VERSION
ENV PATH="/opt/dotnet:${PATH}"

ENV NEOCLI_VERSION 2.1.0
ENV NEOCLI_SHA256 948396DD7EB65A1C9367183C2A9BC9D711EA1AFCD4E5FEEA426FDC4B66BD01B2
ENV NEOCLI_RELEASE neo-cli-centos.7-x64.zip
ENV NEOCLI_DOWNLOAD_URL https://github.com/neo-project/neo-cli/releases/download/v$NEOCLI_VERSION/$NEOCLI_RELEASE

RUN rpmkeys --import file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 \
    && yum -y update \
    && yum -y install unzip libunwind libicu epel-release

RUN rpmkeys --import file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7 \
    && yum -y install leveldb-devel \
    && yum clean all

RUN curl -sSL $DOTNET_SDK_DOWNLOAD_URL --output dotnet.tar.gz \
    && mkdir -p /opt/dotnet && tar zxf dotnet.tar.gz -C /opt/dotnet \
    && rm -rf dotnet.tar.gz

RUN curl -sSL $NEOCLI_DOWNLOAD_URL --output neo-cli-centos.zip \
    && echo "$NEOCLI_SHA256 *neo-cli-centos.zip" | sha256sum -c - \
    && unzip neo-cli-centos.zip -d /opt/ \
    && rm -rf neo-cli-centos.zip

EXPOSE 10333
WORKDIR /opt/neo-cli
ENTRYPOINT [ "dotnet", "neo-cli.dll" ]
