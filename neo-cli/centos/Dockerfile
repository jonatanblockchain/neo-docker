# neo-cli-centos

FROM centos:centos7
MAINTAINER Jonatan <jonatan.blockchain@gmail.com>

ENV DOTNET_SDK_VERSION 2.0.0
ENV DOTNET_SDK_RELEASE dotnet-sdk-2.0.0-linux-x64.tar.gz
ENV DOTNET_SDK_DOWNLOAD_URL https://download.microsoft.com/download/1/B/4/1B4DE605-8378-47A5-B01B-2C79D6C55519/$DOTNET_SDK_RELEASE
ENV PATH="/opt/dotnet:${PATH}"

ENV NEOCLI_VERSION 2.3.5
ENV NEOCLI_SHA256 ED7EFF3D05C49901C6748A8FB53BC1F1ED1287A97392A962747A4D14B7A18BDA
ENV NEOCLI_RELEASE neo-cli-centos.7-x64.zip
ENV NEOCLI_DOWNLOAD_URL https://github.com/neo-project/neo-cli/releases/download/v$NEOCLI_VERSION/$NEOCLI_RELEASE

RUN rpmkeys --import file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 \
    && yum update \
    && yum install -y --setopt=tsflags=nodocs unzip libunwind libicu epel-release \
    && rpmkeys --import file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7 \
    && yum install -y --setopt=tsflags=nodocs leveldb-devel \
    && yum clean all

RUN curl -sSL -o dotnet.tar.gz $DOTNET_SDK_DOWNLOAD_URL \
    && mkdir -p /opt/dotnet && tar zxf dotnet.tar.gz -C /opt/dotnet \
    && rm -rf dotnet.tar.gz

RUN curl -sSL -o neo-cli-centos.zip $NEOCLI_DOWNLOAD_URL \
    && echo "$NEOCLI_SHA256 *neo-cli-centos.zip" | sha256sum -c - \
    && unzip neo-cli-centos.zip -d /opt/ \
    && rm -rf neo-cli-centos.zip


EXPOSE 10333
WORKDIR /opt/neo-cli
ENTRYPOINT [ "dotnet", "neo-cli.dll" ]
