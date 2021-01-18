FROM jenkins/jenkins:lts-jdk11

ENV CURL_OPTIONS -sSfLk

USER root
RUN apt-get update && \
    apt-get install -y apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

RUN curl -fsSL -k https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
RUN apt-get update && \
    apt-get install -y docker-ce \
    docker-ce-cli \
    containerd.io \
    maven \
    git \
    && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/{apt,dpkg,cache,log} && \
    usermod -aG docker jenkins && \
    usermod -aG sudo jenkins && \
    add-apt-repository --remove "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

USER root
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli -f /usr/share/jenkins/ref/plugins.txt


