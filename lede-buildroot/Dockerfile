# /dl - the download repo, /lede - the LEDE.git root,
#
#
FROM		debian:stable
LABEL		CMDBUILD="docker build -t njhsi/lede-buildroot https://raw.githubusercontent.com/njhsi/dockerfiles/master/lede-buildroot/Dockerfile"
LABEL		CMDRUN="docker run njhsi/lede-buildroot"

MAINTAINER	njhsi

ENV DEBIAN_MIRROR    http://chinanet.mirrors.ustc.edu.cn/debian
ENV DEBIAN_SECURITY  http://chinanet.mirrors.ustc.edu.cn/debian-security/

RUN echo "deb $DEBIAN_MIRROR stable main contrib" > /etc/apt/sources.list
RUN echo "deb $DEBIAN_SECURITY stable/updates main contrib" >> /etc/apt/sources.list
RUN echo "deb $DEBIAN_MIRROR stable-updates main contrib" >> /etc/apt/sources.list

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
 && apt-get dist-upgrade -y \
 && apt-get install -y locales sudo \
 && rm -rf /var/lib/apt/lists/*

RUN echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen \
 && locale-gen en_US.UTF-8 \
 && update-locale LANG=en_US.UTF-8 LANGUAGE=en_US:en
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8

RUN     apt-get update

# 1 : openwrt
RUN	apt-get install -yq \
			git-core build-essential libssl-dev libncurses5-dev unzip gawk time bc \
			zlib1g-dev flex gettext wget subversion file python-pip python3-dev automake bison patchelf findutils rsync \
			sudo squashfs-tools emacs-nox libglib2.0-dev \
			less openssh-client file \
            --no-install-recommends 

#1 : coreelec
#RUN apt-get install -yq \
#    wget bash bc gcc sed patch patchutils tar bzip2 gzip perl gawk gperf zip unzip diffutils texinfo lzop python3 python \
#    g++ xfonts-utils xfonts-utils xfonts-utils xsltproc default-jre-headless \
#    libc6-dev libncurses5-dev \
#    u-boot-tools \
#    xz-utils make file libxml-parser-perl \
#    libjson-perl \
#    golang-go \
#    git-core openssh-client \
#    --no-install-recommends

RUN  apt-get clean && rm -rf /var/lib/apt/lists/*

RUN adduser --disabled-password --gecos '' --shell /bin/bash --home /lede buildman
RUN adduser buildman sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER buildman
WORKDIR /lede

