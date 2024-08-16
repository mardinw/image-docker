FROM docker.io/alpine:latest

# Set env version variables
ENV ASTERISK_VERSION=21.3.1

RUN apk add --no-cache \
	build-base \
	wget \
	ncurses-dev \
	openssl-dev \
	libxml2-dev \
	jansson-dev \
	unixodbc-dev \
	tar \
	sqlite-dev \
	curl \
	pcre-dev \
	util-linux-dev

RUN apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing \
    pjproject-dev \
    libuuid

# Work for asterisk
WORKDIR /usr/src/asterisk

# copy file tar.gz from local to image
COPY asterisk-${ASTERISK_VERSION}.tar.gz .

RUN tar -xzvf asterisk-${ASTERISK_VERSION}.tar.gz && \
	cd asterisk-${ASTERISK_VERSION} && \
	./configure --with-jansson-bundled && \
	make && \
	make install && \
	make samples && \
	make config

# set configuration for asterisk
RUN ldconfig && \
	adduser -D asterisk && \
	chown asterisk /var/run/asterisk && \
	chown -R asterisk /etc/asterisk && \
	chown -R asterisk /var/{lib,log,spool}/asterisk && \
	chown -R asterisk /usr/lib/asterisk

# expose port
EXPOSE 5060 5061 4569

USER asterisk

# running asterisk
CMD ["/usr/sbin/asterisk", "-f", "-U", "asterisk"]
