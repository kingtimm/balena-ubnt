FROM alpine:latest

WORKDIR /usr/src/app

ENV DDCLIENT_VERSION=ab706ccae039cc5144c6ef77700285f5c1c4645e
RUN apk add perl git wget curl make gcc openssl perl-dev musl-dev openssl-dev zlib-dev perl-app-cpanminus
RUN cpanm Data::Validate::IP Net::SSLeay IO::Socket::SSL
RUN git clone https://github.com/ddclient/ddclient.git ddclient-cloudflare \
	&& cd ddclient-cloudflare \
	&& git checkout -b build "${DDCLIENT_VERSION}" \
	&& cp ddclient /usr/sbin \
	&& mkdir -p /etc/ddclient /var/cache/ddclient

COPY conf/ddclient.conf /etc/ddclient/ddclient.conf
RUN chmod 600 /etc/ddclient/ddclient.conf
COPY setup-and-run.sh /usr/src/app

RUN chmod +x /usr/src/app/setup-and-run.sh

CMD ["./setup-and-run.sh"]
