FROM nginx:latest

# Install a password file creation utility to create username-password pairs
RUN apt-get update; apt-get install -y --no-install-recommends apache2-utils

RUN mkdir /etc/apache2; cd /etc/apache2; touch .htpasswd