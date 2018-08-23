FROM jenkins/jenkins:lts-alpine

LABEL maintainer="Orbis Mobile Team"

# Preinstalling plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Global variable for Fastlane
ENV FASTLANE_BIN /usr/local/bin

# Configuring reverse proxy
ENV JENKINS_OPTS="--prefix=/jenkins"

# Define the android home path
ENV ANDROID_HOME /usr/share/jenkins/ref/sdk

ARG ANDROID_SDK_URL_FOR_LINUX=https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip

RUN mkdir -p $ANDROID_HOME

RUN curl -o $ANDROID_HOME/sdk.zip ${ANDROID_SDK_URL_FOR_LINUX}

RUN unzip -d $ANDROID_HOME $ANDROID_HOME/sdk.zip

RUN rm -rf $ANDROID_HOME/sdk.zip

RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "tools" "extras;android;m2repository" \
"extras;google;m2repository" "platform-tools" "platforms;android-27" "build-tools;27.0.1" \
"extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2" \
"extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2" 
#"cmake;3.6.4111459" "ndk-bundle"

# if we want to install via apt
USER root

#RUN apk add build-base

RUN apk update && \
    apk add --no-cache \
        ruby \
        ruby-rdoc \
        ruby-irb \
        ruby-dev \ 
        g++ \
        make

# install glibc for alpine
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.26-r0/glibc-2.26-r0.apk
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.26-r0/glibc-bin-2.26-r0.apk
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.26-r0/glibc-i18n-2.26-r0.apk

RUN apk add --no-cache --allow-untrusted glibc-2.26-r0.apk
RUN apk add --no-cache --allow-untrusted glibc-bin-2.26-r0.apk
RUN apk add --no-cache --allow-untrusted glibc-i18n-2.26-r0.apk

RUN /usr/glibc-compat/bin/localedef -i en_US -f UTF-8 en_US.UTF-8

RUN gem install fastlane -NV

#Google Cloud SDK
#RUN echo Y | apt-get install lsb-release

#RUN export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
#    echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
#    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
#    apt-get update

#RUN echo Y | apt-get install google-cloud-sdk

#RUN echo n | gcloud init

# drop back to the regular jenkins user - good practice
USER jenkins