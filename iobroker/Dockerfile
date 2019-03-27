FROM ubuntu:18.04

MAINTAINER Andreas Wegscheider <it-services@samjas.eu>


# ENV
ENV TZ Europe/Vienna
ENV IOBROKER_VERSION 2.0.2
ENV NODEJS_VERSION 8.x
ENV LANG de_AT.UTF-8
ENV LANGUAGE de_AT.UTF-8
ENV LC_ALL de_AT.UTF-8
ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm


# PRES
RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y \
	acl \
	build-essential \
	curl \
	git \
	libcap2-bin \
	libavahi-compat-libdnssd-dev \
	libudev-dev \
	libpam0g-dev \
	locales \
	net-tools \
	nodejs \
	npm \
	python \
	sudo \
	tzdata \
	unzip \
	vim \
	wget

# NODE.JS
RUN curl -sL https://deb.nodesource.com/setup_$NODEJS_VERSION | sudo -E bash -
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y nodejs


# TIMEZONE
RUN locale-gen $LANG
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata



# IOBROKER
WORKDIR /
RUN apt-get update \
		&& echo $(hostname) > /opt/iobroker/.install_host \
    && curl -sL https://iobroker.net/install.sh | bash - \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /opt/iobroker
#RUN npm install -g node-gyp

RUN tar -cf /opt/initial_iobroker.tar /opt/iobroker

#RUN echo 'iobroker ALL=(ALL) NOPASSWD: ALL' | EDITOR='tee -a' visudo \
#    && echo "iobroker:iobroker" | chpasswd \
#    && adduser iobroker sudo
#USER iobroker



EXPOSE 8081/tcp
EXPOSE 8082/tcp

#ENTRYPOINT ["sh", "/opt/iobroker/scripts/start.sh"]
#ENTRYPOINT ["sudo", "iobroker", "start"]
