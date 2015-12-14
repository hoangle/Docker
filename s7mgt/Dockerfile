# sshd
#
# VERSION               0.0.1

FROM     ubuntu:14.04

MAINTAINER hoang "hoang.le@openclovis.com" 

# make sure the package repository is up to date
RUN apt-get update

RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:clovis' |chpasswd

RUN apt-get update && apt-get install -y \
    unzip \
    libprotoc-dev \
    protobuf-compiler \
    python-protobuf \
    libbz2-dev \
    python-dev \
    g++ \
    libboost1.55-all-dev \
    libdb-dev \
    libgdbm-dev \
    libsqlite3-dev \
    dh-make \
    libxml2-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get install -y \
    libprotobuf-dev=2.5.0-9ubuntu1 \
    libprotobuf-lite8=2.5.0-9ubuntu1 \
    libprotobuf8=2.5.0-9ubuntu1 \
    libprotoc-dev=2.5.0-9ubuntu1 \
    libprotoc8=2.5.0-9ubuntu1 \
    protobuf-compiler=2.5.0-9ubuntu1

RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

COPY ./netconf-subsystem /etc/init.d/netconf-subsystem

# Listen to netconf service
RUN echo "Port 830"  >> /etc/ssh/sshd_config
RUN echo "Subsystem netconf /etc/init.d/netconf-subsystem" >> /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22 830
CMD    ["/usr/sbin/sshd", "-D"]
