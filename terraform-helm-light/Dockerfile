FROM hashicorp/terraform:light

# Install selected extensions and other stuff
ENV HELM_VERSION=3.1.2
ENV HELM_FILENAME=helm-v${HELM_VERSION}-linux-amd64.tar.gz
RUN apk update \
  && apk add --update ca-certificates bash openssh curl \
  && apk add --update -t deps wget \
  && wget https://get.helm.sh/${HELM_FILENAME} -P /tmp \
  && tar -zxvf /tmp/${HELM_FILENAME} -C /tmp \
  && mv /tmp/linux-amd64/helm /usr/local/bin \
  && git config --global core.editor vim \
  && rm -f /tmp/${HELM_FILENAME} \
  && apk del --purge deps \
  && rm /var/cache/apk/* \
  && rm -rf /tmp/* \
  && rm -rf /var/cache/apk/* \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /var/tmp/*

ENTRYPOINT [ "/bin/bash" ]
CMD [ "-c", "$@" ]
