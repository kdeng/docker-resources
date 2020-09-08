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

ENV TERRAFORM_VERSION=0.12.25
RUN cd /tmp && \
    wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /usr/local/bin

RUN apt-get purge wget unzip -y && \
  apt-get autoremove -y && \
  apt-get clean -y

RUN  rm -rf /tmp/* && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/tmp/*

ENTRYPOINT [ "/bin/bash" ]
CMD [ "-c", "$@" ]
