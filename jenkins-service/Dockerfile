FROM jenkins/jenkins:lts-alpine

LABEL maintainer="Orbis Mobile Team"

# Preinstalling plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Global variable for Fastlane
ENV FASTLANE_BIN /usr/local/bin

# Configuring reverse proxy
ENV JENKINS_OPTS="--prefix=/jenkins"

