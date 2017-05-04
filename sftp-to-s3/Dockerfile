FROM alpine:3.5

ARG S3FS_VERSION=v1.79

MAINTAINER Simone Esposito <chaufnet@gmail.com>

COPY entrypoint /

RUN apk add --no-cache openssh openssh-sftp-server dropbear &&\
	rm -rf /var/cache/apk/* &&\
	mkdir /etc/dropbear &&\
	touch /var/log/lastlog	&&\
	chmod +x /entrypoin&&t

RUN apk --no-cache add fuse alpine-sdk automake autoconf libxml2-dev fuse-dev curl-dev git bash &&\
    git clone https://github.com/s3fs-fuse/s3fs-fuse.git /tmp/s3fs &&\
    cd /tmp/s3fs &&\
    git checkout tags/${S3FS_VERSION} &&\
    ./autogen.sh &&\
    ./configure --prefix=/usr &&\
    make &&\
    make install &&\
    rm -rf /tmp/*

VOLUME /etc/ssh
EXPOSE 22

ENTRYPOINT ["/entrypoint"]
CMD ["dropbear", "-RFEmwg", "-p", "22"]
