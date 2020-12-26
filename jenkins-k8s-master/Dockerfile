FROM jenkins/jenkins

ENV CURL_OPTIONS -sSfLk

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli -f /usr/share/jenkins/ref/plugins.txt
