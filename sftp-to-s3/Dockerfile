FROM ubuntu:16.04

# Fork of emmekappa/sftp-to-s3

# S3 configuration
ENV AWS_ACCESS_KEY_ID=NotSet \
    AWS_SECRET_ACCESS_KEY=NotSet \
    S3_BUCKET=NotSet \
    DEBIAN_FRONTEND=noninteractive

RUN apt-get update &&\
    apt-get -y --no-install-recommends install openssh-server mime-support build-essential git libfuse-dev libcurl4-openssl-dev libxml2-dev automake libtool pkg-config libssl-dev ca-certificates &&\
    git clone https://github.com/s3fs-fuse/s3fs-fuse /tmp/s3fs-fuse &&\
    cd /tmp/s3fs-fuse &&\
    ./autogen.sh &&\
    ./configure --prefix=/usr --with-openssl &&\
    make &&\
    make install &&\
    mkdir -p /var/run/sshd &&\
    apt-get -y remove build-essential git libfuse-dev libcurl4-openssl-dev libxml2-dev  automake libtool pkg-config libssl-dev ca-certificates &&\
    rm -rf /var/apt/lists/* /tmp/* 

COPY entrypoint /
COPY sshd_config /etc/ssh/sshd_config

RUN chmod +x /entrypoint

EXPOSE 22
ENTRYPOINT ["/entrypoint"]
