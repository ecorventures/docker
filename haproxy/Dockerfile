FROM haproxy
MAINTAINER Corey Butler <corey@coreybutler.com> (@goldglovecb)

RUN groupadd haproxy \
    && useradd -M -g haproxy haproxy

# Install NodeJS
RUN apt-get update
RUN apt-get install -y curl
RUN gpg --keyserver pool.sks-keyservers.net --recv-keys 7937DFD2AB06298B2293C3187D33FF9D0246406D 114F43EE0176B71C7BC219DD50A3051F888C628D

ENV NODE_VERSION 0.12.3
ENV NPM_VERSION 2.10.0
ENV PORT 67890

RUN curl -SLO "http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" \
	&& curl -SLO "http://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
	&& gpg --verify SHASUMS256.txt.asc \
	&& grep " node-v$NODE_VERSION-linux-x64.tar.gz\$" SHASUMS256.txt.asc | sha256sum -c - \
	&& tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 \
	&& rm "node-v$NODE_VERSION-linux-x64.tar.gz" SHASUMS256.txt.asc \
	&& npm install -g npm@"$NPM_VERSION" \
	&& npm cache clear

RUN ls -l
# Expose standard web ports + websocket service
EXPOSE 80 443 ${PORT}

CMD ["haproxy", "-f", "/usr/local/etc/haproxy/haproxy.cfg"]

# FROM mhart/alpine-node:latest
# MAINTAINER Corey Butler <corey@coreybutler.com> (@goldglovecb)
#
# ENV NODE_ENV production
# ENV HAPROXY_MAJOR 1.5
# ENV HAPROXY_VERSION 1.5.12
#
# # RUN apk-install curl gcc libc6-dev libpcre3-dev libssl-dev make
# RUN apk update
# RUN apk upgrade
#
# RUN apk-install pcre-dev openssl-dev linux-headers wget build-base
# RUN wget http://www.haproxy.org/download/$HAPROXY_MAJOR/src/haproxy-$HAPROXY_VERSION.tar.gz -O haproxy.tar.gz \
#     && mkdir -p /usr/src/haproxy \
#     && tar vxzf haproxy.tar.gz -C /usr/src/haproxy \
#     && rm haproxy.tar.gz \
#     && make -C /usr/src/haproxy/haproxy-$HAPROXY_VERSION \
#   		TARGET=linux2628 \
#   		USE_PCRE=1 PCREDIR= \
#   		USE_OPENSSL=1 \
#       #CFLAGS="$CFLAGS" \
#       #CPU=native \
#       #USE_LIBCRYPT=1 \
#       #USE_LINUX_SPLICE=1 \
#       #USE_LINUX_TPROXY=1 \
#   		USE_ZLIB=1 \
# 	&& mkdir -p /usr/local/etc/haproxy \
#   && make install -C /usr/src/haproxy/haproxy-$HAPROXY_VERSION \
# 	&& rm -rf /usr/src/haproxy
#
# RUN addgroup haproxy
# RUN adduser -D -H -G haproxy haproxy
#
# RUN haproxy -v
#
# #WORKDIR /app
#
#
# EXPOSE 80
# EXPOSE 443
#
#
