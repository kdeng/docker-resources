FROM ubuntu:latest

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y openjdk-11-jdk-headless \
    maven \
    git \
    curl
RUN apt-get install -y apt-transport-https
RUN apt-get install -y ca-certificates
RUN apt-get install -y gnupg-agent
RUN apt-get install -y software-properties-common
RUN apt-get install -y iptables
RUN apt-get install -y lxc
RUN apt-get install -y kmod

# RUN mkdir -p /root/.ssh && \
#     chmod 0700 /root/.ssh && \
#     ssh-keyscan github.com > /root/.ssh/known_hosts

# RUN apt-get install -y --reinstall linux-headers-$(uname -r)
# RUN cat <<EOF | sh -x
# RUN modprobe ip_tables
# RUN EOF

RUN addgroup --gid 1000 ebroker && \
    adduser --system --uid 1000 ebroker --gid 1000

# RUN curl -sSL https://get.docker.com/rootless | sh
# RUN export PATH=/home/moby/bin:$PATH
# RUN export DOCKER_HOST=unix:///run/user/1000/docker.sock

RUN curl -fsSL -k https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get remove docker docker-engine docker.io containerd runc && \
    apt-get install -y docker-ce docker-ce-cli containerd.io && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/ && \
    usermod -aG docker root && \
    add-apt-repository --remove "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# USER ebroker
