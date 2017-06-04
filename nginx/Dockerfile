FROM nginx:latest

MAINTAINER Jannik Kühnemundt <jkuehnemundt@gmail.com>

RUN apt-get update && \
    apt-get install -y \
    nginx \
    wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget https://getcomposer.org/composer.phar -P /home/student/htdocs/hansesim
