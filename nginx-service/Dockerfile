FROM nginx:stable-alpine

RUN apk update; apk add --update apache2-utils

#Install a password file creation utility to create username-password pairs
RUN mkdir /etc/apache2; cd /etc/apache2; touch .htpasswd