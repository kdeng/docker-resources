# Use latest google/cloud-sdk image as the base
FROM google/cloud-sdk:latest

# Developer
MAINTAINER Kefeng Deng (deng@51any.com)

# Environment variables
ENV GO_VERSION 1.10.3

# Install Google SDK components
RUN echo -e "\n[INSTALL]: update google cloud components" && \
    apt-get update && \
    apt-get install -y wget && \
    apt-get --only-upgrade install -y \
    google-cloud-sdk \
    google-cloud-sdk-app-engine-go && \
    cd /tmp && \
    wget https://dl.google.com/go/go$GO_VERSION.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go$GO_VERSION.linux-amd64.tar.gz && \
    export PATH="$PATH:/usr/local/go/bin" && \
    export GOPATH=/go && \
    echo -e "\n[INSTALL]: Install go tools" && \
    go get -u -v github.com/julienschmidt/httprouter && \
    go get -u -v google.golang.org/appengine && \
    go get -u -v cloud.google.com/go/bigquery && \
    go get -u -v github.com/googleapis/gax-go && \
    rm /tmp/go$GO_VERSION.linux-amd64.tar.gz && \
    apt-get autoremove && apt-get clean

ENV PATH "$PATH:/usr/local/go/bin"
ENV GOPATH "/go"
