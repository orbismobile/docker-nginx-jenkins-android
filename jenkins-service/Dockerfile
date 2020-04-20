FROM jenkins/jenkins:lts

LABEL maintainer="Orbis Mobile Team"

# Preinstalling plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Configuring reverse proxy
ENV JENKINS_OPTS="--prefix=/jenkins"