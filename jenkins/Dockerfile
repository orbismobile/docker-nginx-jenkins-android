FROM jenkins/jenkins:latest

LABEL maintainer="Orbis Team"

# Change URL for use behind a reserve proy
ENV JENKINS_OPTS="--prefix=/jenkins" 

# Install init.d groovy scripts
#COPY ./init.groovy.d/executors.groovy       /usr/share/jenkins/ref/init.groovy.d/executors.groovy
#COPY ./init.groovy.d/load-properties.groovy /usr/share/jenkins/ref/init.groovy.d/load-properties.groovy

# Install plguins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Avoid banner prompting user to install additional plugins
#RUN echo 2.0 > /usr/share/jenkins/ref/jenkins.install.UpgradeWizard.state

ARG ANDROID_SDK_URL_FOR_LINUX=https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip

ENV ANDROID_HOME /usr/share/jenkins/ref/sdk

RUN mkdir -p $ANDROID_HOME

RUN curl -o $ANDROID_HOME/sdk.zip ${ANDROID_SDK_URL_FOR_LINUX}

RUN unzip -d $ANDROID_HOME $ANDROID_HOME/sdk.zip

RUN rm -rf $ANDROID_HOME/sdk.zip

RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "tools" "emulator" "extras;android;m2repository" \
"extras;google;m2repository" "platform-tools" "platforms;android-27" "build-tools;27.0.1" \
"extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2" \
"extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2" \
"cmake;3.6.4111459" "ndk-bundle"

USER root

RUN apt-get update && apt-get install

RUN echo yes| apt-get install ruby-full

RUN echo yes | apt-get install build-essential

RUN gem install fastlane -NV

USER jenkins

