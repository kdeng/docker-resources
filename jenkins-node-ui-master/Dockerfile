FROM jenkins/jenkins:lts-jdk11

ENV CURL_OPTIONS -sSfLk -C -
ENV JENKINS_UC_DOWNLOAD=http://mirrors.jenkins-ci.org

USER root
RUN apt-get update && \
    apt-get install -y apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

RUN apt-get update && \
    apt-get install -y xvfb libxi6 libgconf-2-4 &&\
    apt-get install -y gnupg wget curl unzip --no-install-recommends && \
    wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list && \
    apt-get update -y && \
    apt-get install -y google-chrome-stable && \
    CHROMEVER=$(google-chrome --product-version | grep -o "[^\.]*\.[^\.]*\.[^\.]*") && \
    DRIVERVER=$(curl -s "https://chromedriver.storage.googleapis.com/LATEST_RELEASE_$CHROMEVER") && \
    wget -q --continue -P /chromedriver "http://chromedriver.storage.googleapis.com/$DRIVERVER/chromedriver_linux64.zip" && \
    unzip /chromedriver/chromedriver* -d /chromedriver

ENV PATH=/chromedriver:$PATH

# Install selected extensions and other stuff
ENV HELM_VERSION=3.6.3
ENV HELM_FILENAME=helm-v${HELM_VERSION}-linux-amd64.tar.gz
RUN wget https://get.helm.sh/${HELM_FILENAME} -P /tmp \
  && tar -zxvf /tmp/${HELM_FILENAME} -C /tmp \
  && mv /tmp/linux-amd64/helm /usr/local/bin \
  && git config --global core.editor vim \
  && rm -f /tmp/${HELM_FILENAME}

RUN cd /tmp && \
    curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl" && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl

RUN curl -fsSL -k https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
RUN apt-get update && \
    apt-get install -y docker-ce \
    docker-ce-cli \
    containerd.io \
    maven \
    git \
    vim \
    && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/{apt,dpkg,cache,log} && \
    usermod -aG docker jenkins && \
    usermod -aG sudo jenkins && \
    add-apt-repository --remove "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

RUN mkdir -p /home/jenkins/.kube && \
    chown -R jenkins:jenkins /home/jenkins

USER jenkins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli -f /usr/share/jenkins/ref/plugins.txt


