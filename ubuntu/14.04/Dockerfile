# DOCKER-VERSION 1.9.1
# VERSION        0.1
# SOURCE         https://github.com/mesosinfo/mesos-master

FROM ubuntu:14.04
MAINTAINER Yong Zhang<zhangyong.net@qq.com>

# Install dependancies
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF && \
echo deb http://repos.mesosphere.io/ubuntu trusty main > /etc/apt/sources.list.d/mesosphere.list && \
apt-get update
RUN sudo apt-get -y install curl python-setuptools python-pip python-dev python-protobuf

# Install mesos.
RUN sudo apt-get -y install mesos
RUN sudo mkdir -p /etc/mesos-master
RUN echo in_memory | sudo dd of=/etc/mesos-master/registry

ENTRYPOINT ["mesos-master"]
