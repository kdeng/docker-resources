FROM gcr.io/cloud-builders/gcloud-slim:latest

RUN apt-get update && \
  apt-get install --no-install-recommends -y \
  curl \
  ca-certificates \
  openssl \
  unzip \
  wget \
  bash \
  vim && \
  apt-get dist-upgrade -y && \
  apt-get autoremove -y && \
  apt-get clean -y && \
  gcloud components install kubectl --quiet && \
  gcloud components update --quiet

# Install selected extensions and other stuff
ENV HELM_VERSION=3.2.1
ENV HELM_FILENAME=helm-v${HELM_VERSION}-linux-amd64.tar.gz
RUN wget https://get.helm.sh/${HELM_FILENAME} -P /tmp \
  && tar -zxvf /tmp/${HELM_FILENAME} -C /tmp \
  && mv /tmp/linux-amd64/helm /usr/local/bin \
  && git config --global core.editor vim \
  && rm -f /tmp/${HELM_FILENAME} \
  && rm -rf /tmp/* \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /var/tmp/*

RUN apt-get purge wget unzip -y && \
  apt-get autoremove -y && \
  apt-get clean -y

RUN  rm -rf /tmp/* && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/tmp/*

ENTRYPOINT [ "/bin/bash" ]
CMD [ "-c", "$@" ]
