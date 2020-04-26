# /dl - the download repo, /openwrt - the openwrt.git root,
#
#
FROM		debian:stable
LABEL		CMDBUILD="docker build -t njhsi/openwrt-buildroot https://raw.githubusercontent.com/njhsi/dockerfiles/master/openwrt-buildroot/Dockerfile"
LABEL		CMDRUN="docker run njhsi/openwrt-buildroot"

MAINTAINER	njhsi

# gettext for envsubst
RUN		apt-get update && \
			apt-get install -yq git-core build-essential libssl-dev libncurses5-dev unzip gawk \
			zlib1g-dev flex gettext wget subversion file python2.7-dev automake bison patchelf findutils libglib2.0-dev \
			sudo && \
			apt-get clean 

RUN adduser --disabled-password --gecos '' --shell /bin/bash --home /openwrt buildman
RUN adduser buildman sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER buildman
WORKDIR /openwrt

#ENTRYPOINT      ["/setup.sh"]
