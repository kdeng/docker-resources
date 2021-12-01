FROM gcr.io/cloud-builders/git

ENV JAVA_HOME "/usr/lib/jvm/java-8-openjdk-amd64/"
ENV PATH "$PATH:$M2_HOME/bin:$JAVA_HOME/bin"
ENV KEYSTORE=${JAVA_HOME}/jre/lib/security/cacerts

RUN add-apt-repository ppa:openjdk-r/ppa && \
	apt-get update -qqy && \
	apt-get install -qqy --no-install-recommends \
		ca-certificates \
		ca-certificates-java \
		vim \
		wget \
		openjdk-8-jdk && \
	apt-get clean && \
	git config --global core.editor vim && \
	update-ca-certificates -f && \
	rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/*

# MAVEN
ARG MAVEN_VERSION=3.6.2
ARG USER_HOME_DIR="/root"
ARG SHA=d941423d115cd021514bfd06c453658b1b3e39e6240969caf4315ab7119a77299713f14b620fb2571a264f8dff2473d8af3cb47b05acf0036fc2553199a5c1ee
ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries

ENV MAVEN_HOME /usr/share/maven

RUN mkdir -p /usr/share/maven /usr/share/maven/ref \
  && curl -fsSL -o /tmp/apache-maven.tar.gz ${BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
  && tar -xzf /tmp/apache-maven.tar.gz -C /usr/share/maven --strip-components=1 \
  && rm -f /tmp/apache-maven.tar.gz \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

# Node
ARG NODE_VERSION=v10.16.3
RUN mkdir /nodejs && curl https://nodejs.org/dist/${NODE_VERSION}/node-${NODE_VERSION}-linux-x64.tar.gz | tar xvzf - -C /nodejs --strip-components=1
ENV PATH $PATH:/nodejs/bin

ENTRYPOINT [ "/bin/bash" ]

CMD [ "-c", "$@" ]

