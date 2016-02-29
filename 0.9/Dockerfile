FROM debian:weezy
MAINTAINER Adam Hawkins <adam@hawkins.io>

ENV THRIFT_VERSION 0.9.3

# Thrift '--gen go' needs gofmt
ENV GOLANG_VERSION=1.6
ENV	GOLANG_DOWNLOAD_URL=https://storage.googleapis.com/golang/go$GOLANG_VERSION.linux-amd64.tar.gz \
	GOLANG_DOWNLOAD_SHA256=5470eac05d273c74ff8bac7bef5bad0b5abbd1c4052efbdbc8db45332e836b0b

RUN buildDeps=" \
		automake \
		bison \
		ca-certificates \
		curl \
		flex \
		g++ \
		libboost-dev \
		libboost-filesystem-dev \
		libboost-program-options-dev \
		libboost-system-dev \
		libboost-test-dev \
		libevent-dev \
		libssl-dev \
		libtool \
		make \
		pkg-config \
	" \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends $buildDeps \
	&& rm -rf /var/lib/apt/lists/* \
	&& curl -SL "http://apache.mirrors.spacedump.net/thrift/$THRIFT_VERSION/thrift-$THRIFT_VERSION.tar.gz" -o thrift.tar.gz \
	&& curl -SL "https://www.apache.org/dist/thrift/$THRIFT_VERSION/thrift-$THRIFT_VERSION.tar.gz.asc" -o thrift.tar.gz.asc \
	&& gpg --keyserver ha.pool.sks-keyservers.net --recv-keys 9782694B8B54B4ADD345E52ABB06368F66B778F9 \
	&& gpg --verify thrift.tar.gz.asc thrift.tar.gz \
	&& mkdir -p thrift \
	&& tar -xzf thrift.tar.gz -C thrift --strip-components=1 \
	&& rm thrift.tar.gz thrift.tar.gz.asc \
	&& cd thrift \
	&& ./configure --without-python --without-cpp \
	&& make -j"$(nproc)" \
	&& make install \
	&& cd .. \
	&& rm -rf thrift \
	&& curl -SL "$GOLANG_DOWNLOAD_URL" -o go.tar.gz \
	&& echo "$GOLANG_DOWNLOAD_SHA256 go.tar.gz" | sha256sum -c - \
	&& tar xzf go.tar.gz \
	&& rm go.tar.gz \
	&& cp go/bin/gofmt /usr/bin/gofmt \
	&& rm -rf go \
	&& apt-get purge -y --auto-remove $buildDeps

CMD [ "thrift" ]
