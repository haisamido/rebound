# DEFAULT OS IMAGE
ARG OS_TAG=docker.io/library/ubuntu:20.04

FROM ${OS_TAG}

RUN apt-get update
RUN apt-get install -y python3 python3-pip

WORKDIR /rebound 

RUN pip3 install numpy matplotlib
RUN pip3 install rebound
RUN pip3 install reboundx

#RUN pip3 install -v -e .

ENV PATH=/usr/bin/:$PATH
