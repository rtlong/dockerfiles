# vim: set expandtab tabstop=2 shiftwidth=2 softtabstop=2:
FROM ubuntu:15.10

# Tell Apt never to prompt
ENV DEBIAN_FRONTEND noninteractive

RUN set -x \
 && echo 'Apt::Install-Recommends "false";' > /etc/apt/apt.conf.d/docker-no-recommends \
 && echo 'APT::Get::Assume-Yes "true";' > /etc/apt/apt.conf.d/docker-assume-yes \
 && echo 'APT::Get::AutomaticRemove "true";' > /etc/apt/apt.conf.d/docker-auto-remove \

 && apt-get update \
 && apt-get install \
       bash \
       build-essential \
       ca-certificates \
       checkinstall \
       curl \
       gnupg \
       gzip \

 && cd /tmp \
 && curl -OL http://downloads.sourceforge.net/project/pcre/pcre/8.38/pcre-8.38.tar.gz \
 && curl -OL http://downloads.sourceforge.net/project/pcre/pcre/8.38/pcre-8.38.tar.gz.sig \
 && gpg --refresh-keys \
 && gpg --recv-keys FB0F43D8 \
 && gpg --verify pcre-8.38.tar.gz.sig \
 && tar -xvzf pcre-8.38.tar.gz
RUN set -x \
 && cd /tmp/pcre-8.38 \
 && ./configure \
 && make
RUN set -x \
 && cd /tmp/pcre-8.38 \
 && checkinstall -D \
     --default \
     --install=no \
     --pkgname=libpcre3 \
     --pkgversion=2:8.38 \
     --maintainer=ryan@rtlong.com
