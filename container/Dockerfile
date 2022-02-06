# DEFAULT OS IMAGE
ARG OS_TAG=docker.io/library/ubuntu:20.04

FROM ${OS_TAG}

RUN apt-get update
RUN apt-get install -y python3 python3-pip

RUN pip3 install numpy matplotlib

RUN pip3 install rebound

ENV PATH=/usr/bin/:$PATH

WORKDIR /rebound 
