FROM openjdk:11.0.8-slim

# Install selected extensions and other stuff
RUN apt-get update \
  && apt-get install -y python3 python3-pip curl \
  && ln -sf /usr/bin/python3 /usr/bin/python \
  && ln -sf /usr/bin/pip3 /usr/bin/pip \
  && rm -rf /tmp/* \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /var/tmp/*

# Node
ARG NODE_VERSION=v12.18.3
RUN mkdir /nodejs && curl https://nodejs.org/dist/${NODE_VERSION}/node-${NODE_VERSION}-linux-x64.tar.gz | tar xvzf - -C /nodejs --strip-components=1
ENV PATH $PATH:/nodejs/bin

ENTRYPOINT [ "/bin/bash" ]
CMD [ "-c", "$@" ]
