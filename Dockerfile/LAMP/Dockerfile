FROM ubuntu:16.04
MAINTAINER Piboonsak Pimsarn (PiboonsakTraceon@gmail.com) 
LABEL Description="ubuntu STD v2.12"
ENV ubuntu=16.04
RUN apt-get update && apt-get install -y \
	nano \
	vim \
	wget \
	curl \
	htop \
	man \
        ufw \
	net-tools \
        iptables iptables-persistent
RUN apt-get install -y iputils-ping
RUN apt-get install -y openssh-server
RUN service ssh restart
RUN mkdir -p /myapp
WORKDIR /myapp
CMD ["/bin/bash"]
EXPOSE 22/tcp 443/tcp 80/tcp 3306/tcp 8080/tcp 8088/tcp 8089/tcp
